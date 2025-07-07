Kubernetes Architecture
-> Cluster
	-> Control Plane (API, ETCD, KUBELET) 
	-> Hosts (Nodes)
		-> Pods
			-> Containers

The scheduler is seen as the brain and decides where the best node is for a pod to go.

The controller manager monitors the state of the cluster it is responsible for many tasks.
- Ensuring pods are running
- Ensuring there is enough pods for a deployment and makes deployments.
- Monitoring nodes health.
- Token and service account management. (Reissuing and creating tokens, and assigning service accounts to namespaces.)

The kubelet
- Responsible for managing containers and resources (CPU, Memory, Etc.) within a pod.
- Ensures containers are running.
- Sends updates to the api on the overall status of a pod. (Logs)
- There is a kubelet inside every pod.

The kube-proxy
- Ensures that services within nodes can communicate with each other and with other services in other nodes.
- Controls network flow between the cluster.
- Essentially a router.
- Network policies or NACLs are assigned on the kubectl level in a YAML file and sent to the ETCD server. They are then assigned in deployment YAML files and assigned to a namespace and label attached to a pod.

Namespace 
- A virtual segmentation of pods. Esenntially like a VLAN
- A namespace is purely logical that is the difference between a VLAN.
- Each namespace contains its own pods, service account, deployments.
- Typical setup is dev, prod, staging, monitoring, and logging.

Service Accounts
- When a service account is created the RBAC is set.
- Tokens and accounts are created and assigned to pods by the controller manager.
- Tokens are typically used to communicate with the api-server in the event there is a service running in a container that needs to such as jenkins.
- All tokens are stored on the ETCD server
- Tokens are deployed on containers inside pods and mounted to /var/run/secrets/kubernetes.io/</serviceaccount>/</token>
## The 4C's of Cloud Native Security

Cloud (Infrastructure)
Cluster (Authentication, Authorisation, Admission, Network Policy)
Container (Restrict Images, Supply Chain, Sandboxing, Privileged)
Code (Secure Code Best Practices)

Cluster Setup and Hardening

#### CIS Benchmark for Kubernetes Server.
- Kube-Bench https://github.com/aquasecurity/kube-bench
- Trivy also supports benchmark scanning.

# Kube API Server


## General Best practices
- Do not use hard coded password or token files.
- Do not use the api directly because then password are in the bash history.
- Use service accounts for 3rd party integrations  - essentially creates an api/bearer token for use.
- service accounts that are local in the cluster can be mounted, that way when the container is spawned the secret is mounted to it, authenticating it. The service account is simply defined in the pod definition yml file.
- Integrate with kerberos or ldap.
## Authentication
- Who can access the cluster?
- Who is accessing the cluster?
	- Admins
	- Developers
	- 3rd Party Integrations
### TLS
- This is a commonly used authentication type in Kubernetes environments to enforce secure authentication that is passwordless.
- All servers listed should have their own certificate and key pair.
- All clients listed should also have their own certificate and key pair to validate their identity to the server.
- Roles and groups are also assigned through object identifiers when creating the certificate signing request.
- All client certificates should be configured and set in the kube-config files. (Anything that wants to talk to the server api)

![[Pasted image 20250629103055.png]]

#### Reviewing TLS Security

##### Mapping TLS Certificates and Keys

First create a spreadsheet to fill out all the information on the TLS:
- https://github.com/mmumshad/kubernetes-the-hard-way/blob/master/tools/kubernetes-certs-checker.xlsx
- https://kubernetes.io/docs/setup/best-practices/certificates/

First check the file paths to the certificates

    ```
    cat /etc/kubernetes/manifests/kube-apiserver.yaml    
    cat /etc/kubernetes/manifests/etcd.yaml
    ```

![[Pasted image 20250629121016.png]]

Second check the certificate details:
- Common Name / Issuer
- Expiry Date
- Alternative names
- Organisation - IMPORTANT!!! Overly permissive can be dangerous here.

    ```
    openssl x509 -in /etc/kubernetes/pki/<cert> -text -noout
    ```

![[Pasted image 20250629121123.png]]

##### Protecting the Root CA
- Should be restricted to only root and certain processes such as the controller manager.
- Defined in the kube-controller-manager.yaml
- Used to sign all new certificates from certificate signing requests.

![[Pasted image 20250629130915.png]]

##### Kube Config File
- Avoid storing entire keys in here, instead reference them by an absolute path.
- Strict permissions on those keys to the user only.
- This avoids keys being accidentally stored in a backup somewhere.
- Use multiple contexts and users if necessary to split permissions and enforce principle of least privilege.

For example below, multiple contexts and users are used, GOOD, keys are referenced by absolute path GOOD.
![[Pasted image 20250629172658.png]]



## Authorization
#### Authorization Modes are Defined.
- Defined in api-server manifest.
- The order does matter.
- Determines which methods are used by the server.

#### Configuring Authorization Modes.
RBAC
- This is the most common approach.
- Each user, service account or server component is binded to a role.
- There is a role file defining the permissions for that role.
	- API Group defined.
	- Then resources in API Group defined.
	- Then methods allowed on resources defined.
- There is a role binding file that binds a subject(s) to a role.

Node

Webhook (OPA)

Always Allow + Always Deny
- Should be avoided and a red flag in most cases.

ABAC
- Also should be avoided this is deprecated by RBAC + OPA

#### Checklist
- Verify cluster roles are not overly permissive.
	- No cluster roles assigned to service accounts.
- Verify service account role bindings are not overly permissive
- Verify user role bindings are not overly permissive (kubectl get rolebindings -A -o yaml  | grep user)

- What can they do?
	- RBAC Authorization
	- ABAC Authorization
	- Node Authorization
	- Webhook mode
	- Principal of least privilege.

Network Policies
- Restricting traffic between containers.

Modes: AlwaysAllow, Node, ABAC, RBAC, Webhook, AlwaysDeny
- The modes to be used are set in the kube-apiserver.yaml manifest.
- Authorisation modes are handled in the order they are specified in.
- AlwaysAllow is a big NO.

How to create a role.
- First create the YAML file.
- Then apply with the following command.
![[Pasted image 20250702195043.png]]
![[Pasted image 20250702195138.png]]

How to bind a role to a user.
![[Pasted image 20250702195618.png]]

![[Pasted image 20250702195840.png]]

Auditing Roles
- Never put sensitive information in the kube-public namespace.
- Be careful with Cluster Roles. As these often give access to resources cluster wide. Especially if given to a service account.

Testing Roles
- Using the can-i to manually test permissions on serviceaccounts, users and namespaces.
![[Pasted image 20250702200043.png]]

#### Securing The Kubelet
All configuration is stored in the kubelet configuration file:
- Check that the API port on 10255 is disabled - this by default allows unauthenticated access read only.
- Check that the API port on 10250 is locked down - again by default allows anonymous access. (in config file anonymous enabled: false)
- Check that the authentication mode in the kubelet config is set to certificate based.
- Check that the authorization mode in the kubetlet config is set to Webhook.

Securing the Dashboard
- How is it being accessed? Is it exposed to the public?
- Best to keep it local and use a jumphost + VPN + OAuth/OpenID.
All configuration is stored in the 
- 

#### Network Policies
- **Kubernetes is configured by default with an ALL ALLOW rule by default between pods.** Allowing network communication between the entire cluster open and possible.
- Policies are linked to one or more pods usually by namespace / label (Pod Selector OR Namespace Selector)
- When selectors are listed separately with dashes this is an OR logic. With just one dash and then multiple selectors this is an AND.
- Ideally each pod has its own network policy applied essentially creating a logical host based firewall. This allows for very refined grained network traffic control
- Don't forget to deny egress from all pods to the cloud node metadata service (this can contain cloud credentials!!)
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: example-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: my-app  # Apply to pods with this label
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
    - namespaceSelector:
        matchLabels:
          team: dev
    - ipBlock:
        cidr: 10.0.0.0/16
        except:
        - 10.0.5.0/24
    ports:
    - protocol: TCP
      port: 80
```

### Ingress

#### Ingress Controller

#### What is it?
- Install one ingress controller per cluster. (Nginx)
- This acts as a proxy for all ingress resources 
- This stops the need for multiple proxies and load balancers.
- Deploy the ingress controller and then create the service object with LoadBalancer. (An external load balancer is then deployed automatically via AWS)
#### Ingress Resources
- Defined just like any other object with kind: Ingress
- These are consumed and routed by the ingress controller.
![[Pasted image 20250704175702.png]]

#### Securing the Ingress
- Apply a strict network policy to the ingress controller namespace. - only allow ingress traffic from pods in other namespaces that need it. Typically the ingress controller only handles incoming requests from the internet not from the internal services.
- Check that ingress resource files map the correct paths and are not exposing more then they should. Avoid catch-all routes.
- Limit roles that can create and modify ingress resources.
- Check security headers are set correctly.
- Check in general any weird web server config details.
### Kubernetes Setup
#### Dashboard Setup

    ```
    kubectl apply -f <link to github yaml>
    ```


#### Commands 
##### Port Forwarding
- Used to reach local services running inside the cluster.
    ```
    kubectl port-forward service/<name> <host_port>:<service_port> &
    
    ```


#### Auditing
There are 4 types of auditing: None, Metadata, Request, Request & Response.