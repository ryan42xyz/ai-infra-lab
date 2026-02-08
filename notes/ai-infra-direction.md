# AI Infra Direction

## Context

LLM-backed systems introduce new dimensions: variable latency, token-based cost, non-deterministic outputs. Traditional infra (SLA, capacity planning, rollbacks) needs adaptation.

## Open questions

**Scheduling**
- Batch vs interactive: when to queue, when to stream
- Priority: user-facing vs background vs eval
- Resource allocation: GPU sharing, preemption, cold start

**Cost**
- Token budgets per user/tenant
- Model routing: when to use small vs large model
- Caching: prompt caching, response caching, embedding caching
- Observability: cost per request, cost per feature

**Reliability**
- Retry semantics for transient failures
- Fallback chains: model A fails, try B, then C
- Circuit breakers for external model APIs
- Rate limiting and backpressure

**Quality**
- Evaluation pipelines: regression tests for non-deterministic outputs
- Canary for LLM changes: A/B on model or prompt
- Monitoring for drift: when do outputs degrade?

## Experiments to run

1. Token budget enforcement at API gateway
2. Prompt caching impact on latency and cost
3. Evaluation pipeline for RAG quality
4. Model routing based on request complexity (cheap classifier → expensive model only when needed)

## Non-goals

- Training infra (separate domain)
- Fine-tuning pipelines (separate domain)
- Generic "AI strategy" — focus on infra and ops
