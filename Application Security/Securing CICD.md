---
aliases:
  - Securing CI/CD
---
### How to implement a tool effectively
#### 1 Identify the security gap
- Make a gap analysis.
- Why is this tool actually needed?
- Identify in application security roadmap.

#### 2 Evaulate and assess the tool.
- Integration options.
- Cost/Benefits
- Security

#### 3 Roll out the tool to the test group.
- A small set of development teams.

#### 4 Track Key Metrics
- Pipeline Run Time Impact
	- Track job run times and pipeline durations.
- False Positive Rate
	- Must be manually recorded somewhere
- Stability
	- How often does the tool cause the pipeline to fail.
	- Can be tracked in most CI/CD platforms.
- Developer Feedback
	- Use surveys
	- Hold meetings with the test group for feedback.
- Security Gate Pass Rate
	- Failure rate can be checked in the pipeline/job logs.

#### 5 Optimise the Tool.
- Optimise based on key metric results and development feedback.

#### 6 Integrate into Production.
- Once the tool has proved its stability, accuracy and value.