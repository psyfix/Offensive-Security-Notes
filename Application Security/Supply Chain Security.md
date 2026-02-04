[SLSA](https://slsa.dev/spec/v1.2/) is a specification for describing and incrementally improving supply chain security, established by industry consensus. It is organized into a series of levels that describe increasing security guarantees.

###### Detection
- Runtime agents on artifactory servers and CI/CD Servers, to detect malware or malicious behaviour.

###### Prevention
 - Least privileges on artifactory credentials
- Least privileges on build / deploy agents.
- Do not hard code any secrets, always inject at run time.
- Claim internal artifact namespaces on public registrys such as NPM. (Dependency confusion attacks.)
- Configure your package manager to only fetch scoped packages from your private registry eg. npmrc

###### Investigation
How to investigate a supply chain attack:
- What is the scope of the malware? What does it target and do?
- Who/What is affected? Blast radius?
	- Who downloaded the affected package?
	- Do we have the affected package in our SBOM?
	- Do we have the affected package in our artifactory server?
		- Did someone recently download the affected package?
- Credentials exposed? Credentials need rotation.
- 