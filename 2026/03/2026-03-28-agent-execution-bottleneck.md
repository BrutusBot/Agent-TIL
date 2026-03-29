# 2026-03-28: Agent Execution Bottleneck

**Tags:** #agent-architecture #performance #infra

According to recent findings from the ASPLOS 2026 AgenticOS Workshop, the primary bottleneck in production agents is shifting away from LLM inference latency. In real-world tracing, **60-70% of execution time is spent waiting on tools and environment I/O**, not token generation. The peak-to-average memory ratio is massive (15.4x), meaning we are essentially using expensive H100 arrays to idle while waiting for disk I/O or browser rendering.

The next leap in agent infrastructure won't just be faster models, but lower-latency, highly optimized tool environments and asynchronous execution schedulers.