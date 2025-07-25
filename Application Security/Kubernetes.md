###  Architecture
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
#### The 4C's of Cloud Native Security

Cloud (Infrastructure)
Cluster (Authentication, Authorisation, Admission, Network Policy)
Container (Restrict Images, Supply Chain, Sandboxing, Privileged)
Code (Secure Code Best Practices)

Cluster Setup and Hardening

#### CIS Benchmark for Kubernetes Server.
- Kube-Bench https://github.com/aquasecurity/kube-bench
- Trivy also supports benchmark scanning.


### Administrating 
##### Port Forwarding
- Used to reach local services running inside the cluster.
    ```
    kubectl port-forward service/<name> <host_port>:<service_port> &
    
    ```

### Server Hardening
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
Modes: AlwaysAllow, Node, ABAC, RBAC, Webhook, AlwaysDeny
- The modes to be used are set in the kube-apiserver.yaml manifest.
- Authorisation modes are handled in the order they are specified in.
- AlwaysAllow is a big NO.

### General Best practices
- Do not use hard coded password or token files.
- Do not use the api directly because then password are in the bash history.
- Use service accounts for 3rd party integrations  - essentially creates an api/bearer token for use.
- service accounts that are local in the cluster can be mounted, that way when the container is spawned the secret is mounted to it, authenticating it. The service account is simply defined in the pod definition yml file.
- Integrate with kerberos or ldap.
### Authentication
#### TLS
- This is a commonly used authentication type in Kubernetes environments to enforce secure authentication that is passwordless.
- All servers listed should have their own certificate and key pair.
- All clients listed should also have their own certificate and key pair to validate their identity to the server.
- Roles and groups are also assigned through object identifiers when creating the certificate signing request.
- All client certificates should be configured and set in the kube-config files. (Anything that wants to talk to the server api)

![[Pasted image 20250629103055.png]]
##### Securing Certificates
First create a spreadsheet, a matrix essentially mapping all Kubernertes components:
- https://github.com/mmumshad/kubernetes-the-hard-way/blob/master/tools/kubernetes-certs-checker.xlsx
- https://kubernetes.io/docs/setup/best-practices/certificates/

Use the official documentation as a reference for best practices, on where keys should be stored, with what CNAME and O identifiers.

First check the file paths to the certificates, these can often be found inside the main api-server manifest.

    ```
    cat /etc/kubernetes/manifests/kube-apiserver.yaml    
    cat /etc/kubernetes/manifests/etcd.yaml
    ```

Second check the certificate details:
- Common Name / Issuer - This should be a known trusted CA.
- Expiry Date - is it expired?
- Alternative names
- Organisation - IMPORTANT!!! Overly permissive can be dangerous here.

    ```
    kubectl get secrets --all-namespaces -o json \ | jq -r '.items[] | select(.type=="kubernetes.io/tls") | "\(.metadata.namespace)/\(.metadata.name)"'
    
    openssl x509 -in /etc/kubernetes/pki/<cert> -text -noout
    ```

Third check that certificates are stored correctly:
- An appropriate location, not overly permissive.
- Not inside the kube config file. - This avoids keys being backed up accidentally somewhere.
###### Protecting the Root CA
- Should be restricted to only root and certain processes such as the controller manager.
- Defined in the kube-controller-manager.yaml
- Used to sign all new certificates from certificate signing requests.
###### Kube Config File
- Avoid storing entire keys in here, instead reference them by an absolute path.
- Strict permissions on those keys to the user only.
- This avoids keys being accidentally stored in a backup somewhere.
- Use multiple contexts and users if necessary to split permissions and enforce principle of least privilege.
### Authorization & RBAC

Auditing Roles
- Never put sensitive information in the kube-public namespace.
- Be careful with Cluster Roles. As these often give access to resources cluster wide. Especially if given to a service account.

Testing Roles
- Using the can-i to manually test permissions on serviceaccounts, users and namespaces.

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
### Network 
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

#### Ingress

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

### Operations

Audit & Logging

#### Auditd
#### API Server Auditing
There are 4 types of auditing: None, Metadata, Request, Request & Response.

Monitoring & Detection
Falco
Datadog
Aqua Trace

### Admission Controllers
- These are defined policies that become part of the authorisation process when an api request is made.
- Defined in the kube-apiserver.yaml manifest using the --enable-admission-plugins option.
- Two types of admission controlling, mutation and validation - one can edit a request and one can validate and deny/allow a request.
- Mutating and Validation Admission Webhook exists to integrate external policies that are not built into Kubernetes.

![[Pasted image 20250722110233.png]]

#### Pod Security Admission
This is one of the admission controllers that is enabled by default.
- These are scoped to a namespace.
- There are three out the box ready profiles to use (Restricted, Baseline, Privileged) https://kubernetes.io/docs/concepts/security/pod-security-standards/
- There are three out the box ready modes to use (Enforce, Audit, Warn)
- Possible to write custom policies and apply also.

Setting a cluster wide AdmissionConfiguration object:
![[Pasted image 20250722181516.png]]

Adding a PSA to a specific namespace:
    ```
    kubectl label ns <namespace> \ pod-security.kubernetes.io/<mode>=<profile>
    ```

#### Open Policy Agent / OPA Gate Keeper (WebHook Security Admission)

##### Typical methodology.
- Define Security Requirements (Threat model, CIS, ISO 27001)
	- Typically these match CIS benchmark.
- Create OPA rego policy. -> Audit mode first.
- Create test for OPA rego policy. (Positive, Negative and Edge cases.)
- Run tests locally in cli with opa test.
- PR to feature branch happens -> reviewer also runs tests and check logic.
- Merge to development branch, then triggers build.
- Pipeline build runs.q
- Check kubernetes audit / log artifact from the build.
- Switch to enforce mode.
- Promote to staging or prod.

##### OPA Templates
- https://github.com/open-policy-agent/gatekeeper-library
- A library of templates to use.
###### Playground / Sandbox
https://play.openpolicyagent.org/


#### Security Contexts
- These are security configurations and settings that are defined in Pod Definition files.
- Can either be defined at the Pod level or Container level. Container always takes priority if the same context setting is defined in both but differently.
- Capabilities are only defined at the container level because they give special permissions to perform operations on the underlying node.

runAsUser: </user-id>
- Always needs to be specified otherwise defaults to root.

privileged: true
- bad forces to run as root.

hostPath:
- This is dangerous because it mounts a volume from the underlying node.
- when mounting always use readOnly: True where possible to avoid write permissions.