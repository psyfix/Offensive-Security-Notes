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

#### TLS
- This is a commonly used authentication type in Kubernetes environments to enforce secure authentication that is passwordless.
- All servers listed should have their own certificate and key pair.
- All clients listed should also have their own certificate and key pair to validate their identity to the server.
- Roles and groups are also assigned through object identifiers when creating the certificate signing request.
- All certificates should be configured and set in the kube-config files.

![[Pasted image 20250629103055.png]]
Showing typical certificate setup for a Kubernetes server.

![[Pasted image 20250629105039.png]]
Showing typical certificate config in the kube-config files.
### Servers
KUBE-API Server
ETCD Server
Kubelet Server

### Clients
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