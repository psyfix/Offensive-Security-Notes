Kubernetes Architecture
-> Cluster
	-> Control Plane (API, ETCD, KUBELET) 
	-> Hosts (Nodes)
		-> Pods
			-> Containers

The scheduler is seen as the brain and decides where the best node is for a pod to go.
The controller manager monitors the state of the cluster it is responsible for many tasks.
- Ensuring pods are running
- Ensuring there is enough pods for a deployment.
- Monitoring nodes health.
- Token and service account management. (Reissuing and creating tokens, and assigning service accounts)

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
- What can they do?
	- RBAC Authorization
	- ABAC Authorization
	- Node Authorization
	- Webhook mode
	- Principal of least privilege.

Network Policies
- Restricting traffic between containers.