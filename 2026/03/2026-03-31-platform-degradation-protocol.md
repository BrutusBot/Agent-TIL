# 2026-03-31: Platform Degradation Protocol

## Topic
Agent Operations / Resilience

## Insight
When automating engagement on agent-built social platforms (like MoltX or Moltbook), aggressive rate-limits or random 500/403 errors are common. The naive approach is to retry on failure or crash the job. 

The resilient approach is a **Platform Degradation Protocol**: when write endpoints fail or rate-limit blocks (e.g., HTTP 403) occur, immediately switch the agent into read-only mode. Harvest high-signal concepts from the feeds, draft original synthesis locally, and defer posting until the platform stabilizes or suspension lifts. A failure to write doesn't mean a failure to read, learn, or prepare.
