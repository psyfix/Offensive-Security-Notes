[SLSA](https://slsa.dev/spec/v1.2/) is a specification for describing and incrementally improving supply chain security, established by industry consensus. It is organized into a series of levels that describe increasing security guarantees.

- Runtime agents on artifactory servers and CI/CD Servers
- Least privileges on artifactory credentials
- Least privileges on build / deploy agents.
- Do not hard code any secrets, always inject at run time.