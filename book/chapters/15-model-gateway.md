# Chapter 15. Model gateway

Status: scaffold. Case framing and design plan only; the chapter is unfinished and unvalidated. Updated: 2026-11-10.

[Previous: Chapter 14](./14-resuming-chat.md) · [Table of contents](../table-of-contents.md) · [Next: Chapter 16](./16-simulated-users.md)

**New in this chapter:** token-based rate limits and per-tenant quotas; routing by model tier and by prompt-cache affinity; fallback and hedged requests when every duplicate is billed; usage metered once across retries and cancelled streams.

**Assumes:** hosted model APIs with published rate limits and usage reports; the application trains nothing. A self-hosted open-weight model enters only as one more routing target.

**Reuses:** batching and prompt caching (chapter 4); budgets with uncertain spend (chapter 7); attempts, cancellation, and replay (chapter 14).

> **About the examples.** The product, its tenants, the limits, and every price planned for this chapter are fictional.

## The case

A multi-tenant assistant shares one provider account. At 09:00 one tenant starts a bulk import that sends thousands of summarization requests. Those requests use the account's whole tokens-per-minute allowance, and every other tenant's chat returns rate-limit errors until the import ends.

Earlier chapters treated the model as one endpoint with unlimited capacity. Here capacity is finite, it is counted in tokens, and several products and tenants compete for it. The gateway decides which request runs, on which model, and who pays. It does not change prompts or judge answers.

## The two paths

Path A is a client library inside each service, with its own keys, retries, and limits. Path B is a shared gateway that owns the provider keys, enforces quotas, routes requests, and records usage. The chapter will compare them on the bulk-import fixture and state the traffic level at which the gateway earns its extra hop.

## What the chapter will build

The planned sections follow the limitations in order: one tenant starving the rest (token buckets per tenant, with interactive traffic ahead of batch); a cheap request sent to an expensive model (routing by tier); a cached prompt prefix that misses because requests spread across backends (cache-affinity routing); a provider that slows down (fallback, and hedging priced in tokens); and a bill that counts a retried stream twice (metering by attempt).

The system design it will cover: distributed rate-limit counters, admission and load shedding, estimating output tokens before a request is admitted, and failover between providers and regions.

The fixture, the two paths, the failure drill, and the evaluation plan are still to be designed.

Chapter 16 keeps chapter 14's attempt record and tests the application with simulated users whose success has to be judged by something other than the application's own completion message.

## Sources

No source has been reviewed for this chapter yet.

