# Sample issue: scan for target clients

## Task Spec
- `task_id`: sample-target-scan-001
- `task_type`: research
- `objective`: Identify high-fit companies whose current signals suggest a need for consulting engagement.
- `business_context`: The goal is to expand the target-client list in ways that can realistically feed the consulting pipeline and stabilize revenue.
- `audience`: Internal only
- `inputs[]`:
  - state/02_target_clients/target-client-tracker.csv
  - state/01_consulting_pipeline/consulting-pipeline.csv
  - Current market or web research
- `hard_constraints[]`:
  - Separate verified facts from hypotheses.
  - Preserve factual accuracy in every proposed outreach angle.
- `soft_preferences[]`:
  - Prioritize companies with visible AI, search, marketing, or sales exposure.
- `required_outputs[]`:
  - Proposed target-client rows
  - Any related pipeline-row proposals
  - Commercial rationale summary
- `forbidden_changes[]`:
  - No fabricated risk signals or buyer identities
- `active_agents[]`:
  - target-client-research
  - consulting-pipeline
  - validator
- `status`: ready
- `owner`: tbar88
- `notes`: Route: Business Orchestrator -> target-client-research + consulting-pipeline -> validator -> single user response.
