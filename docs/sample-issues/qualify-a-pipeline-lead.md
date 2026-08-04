# Sample issue: qualify a pipeline lead

## Task Spec
- `task_id`: sample-pipeline-qualify-001
- `task_type`: strategy
- `objective`: Decide whether a target company should be advanced into the active consulting pipeline and define the next revenue-relevant step.
- `business_context`: A potential lead shows AI/search/marketing exposure, but the commercial fit, warm path, and urgency still need to be validated.
- `audience`: Internal only
- `inputs[]`:
  - state/01_consulting_pipeline/consulting-pipeline.csv
  - state/02_target_clients/target-client-tracker.csv
  - Research notes or referral context
- `hard_constraints[]`:
  - Do not convert speculation into verified facts.
  - Keep tracker history intact unless new evidence supports a change.
- `soft_preferences[]`:
  - Prefer next actions that can move revenue within 30 days.
- `required_outputs[]`:
  - Updated or proposed consulting-pipeline row
  - Fit assessment and next action
  - List of evidence gaps
- `forbidden_changes[]`:
  - No fabricated contact, budget, or urgency data
- `active_agents[]`:
  - consulting-pipeline
  - target-client-research
  - validator
- `status`: ready
- `owner`: tbar88
- `notes`: Route: Business Orchestrator -> target-client-research + consulting-pipeline -> validator -> single user response.
