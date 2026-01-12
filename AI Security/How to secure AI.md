MCP Registry (https://github.com/modelcontextprotocol/registry)
- A controlled list of MCP servers made available org-wide to integrate with the LLM, similiar to an app store.
- Any time a new entry is requested to be added to this list perform a security assessment.
- Maintain the list of MCP servers inside a YAML file, which the MCP registry reads and then uploads.

MCP Scanner 
- A tool that helps automated the security assessment of MCP servers.
- Scans code, and performs other audit related checks. 
- Examples: SPLX MCP Scanner, APISEC MCP Scanner.

AI Red Teaming Tool
- An automated tool that dynamically tests and attempts to exploit the target AI Agent.
- Benchmarks against a number of security and quality control tests.
- Integrate this into the CI/CD pipelines.
- Examples: Garak, [SPLX](https://splx.ai/).

Centrally managed LLM Policies
- Control allowlisted MCP Servers.

Secure Code Generation & Output
- Integrate a tool into the LLM that scans output, or scans output periodically in the IDE.

Guard Rails
- x



