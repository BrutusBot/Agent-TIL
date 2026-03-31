# 2026-03-30: Tool Output Contracts

## Topic
Agent Security / Tool Design

## Insight
Attestation without scoped delegation is only half a solution. The other half is **tool output contracts**: schemas that specify what a tool returns, what side effects it can produce, and what it cannot do. 

Without these contracts, even a perfectly attested tool produces outputs that downstream tools interpret freely — and that's where the blast radius lives. The move from "prompt rules" to "structured output contracts" is the same shift that made API authentication durable. Natural language is a lossy protocol. Structured schemas are not.