## The 4C's of Cloud Native Security

Cloud (Infrastructure)
Cluster (Authentication, Authorisation, Admission, Network Policy)
Container (Restrict Images, Supply Chain, Sandboxing, Privileged)
Code (Secure Code Best Practices)

Cluster Setup and Hardening

#### CIS Benchmark for Kubernetes Server.
- Kube-Bench https://github.com/aquasecurity/kube-bench
- Trivy also supports benchmark scanning.

##### Kube API Server

Authentication
- Who can access the cluster?
- Who is accessing the cluster?
	- Admins
	- Developers
	- 3rd Party Integrations

Best practices
- Do not use hard coded password or token files.
- Do not use the api directly because then password are in the bash history.
- Use service accounts for 3rd party integrations  - essentially creates an api/bearer token for use.
- service accounts that are local in the cluster can be mounted, that way when the container is spawned the secret is mounted to it, authenticating it. The service account is simply defined in the pod definition yml file.
- Integrate with kerberos or ldap.

### TLS
- This is a commonly used authentication type in Kubernetes environments to enforce secure authentication that is passwordless.
- All servers listed should have their own certificate and key pair.
- All clients listed should also have their own certificate and key pair to validate their identity to the server.
- Roles and groups are also assigned through object identifiers when creating the certificate signing request.
- All client certificates should be configured and set in the kube-config files. (Anything that wants to talk to the server api)

![[Pasted image 20250629103055.png]]
Showing typical certificate setup for a Kubernetes server.

#### Servers
#### API Server Configuring Server Certificate
- When generating the api-server certificate it is important to list all the different names it may be called by other clients.
![[Pasted image 20250629105907.png]]
- When executing the server it is important to include all the client server certificates for ETCD and Kubelet
![[Pasted image 20250629110713.png]]

##### API Server Defining TLS Clients
![[Pasted image 20250629105039.png]]
- All clients connecting to and communicating with the API Server should be defined in here.

ETCD Server

Kubelet Server
- Each node within the kubelet requires its own certificate.
- The node certificates should include the group object SYSTEM:NODES
- The node certificates are then defined within the kubelet-config file.

#### Clients
Scheduler
Administrators
Kube Controller Manager
Kube Proxy



Authorization
- What can they do?
	- RBAC Authorization
	- ABAC Authorization
	- Node Authorization
	- Webhook mode
	- Principal of least privilege.

Network Policies
- Restricting traffic between containers.

#### Reviewing TLS Security

First check the file paths to the certificates

    ```
    cat /etc/kubernetes/manifests/kube-apiserver.yaml
    ```

![[Pasted image 20250629121016.png]]

Second check the certificate details.


    ```
    cat /etc/kubernetes/manifests/kube-apiserver.yaml
    ```

![[Pasted image 20250629121123.png]]