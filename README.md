# HumanMirror

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

HumanMirror is a Toulouse, France-based agent-infrastructure provider (operated as an entrepreneur individuel) that sells security, verification, data-quality and payment-orchestration services to autonomous agents and the developers who run them. Agents pay per call in USDC on Base through x402 V2 (0.001 / 0.010 / 0.050 USDC tiers, 5 USDC bundles, a 297 USDC 30-day pass) or in Stripe-bought credits (Oracle, Forge, Nexus); humans buy audits, a Pro subscription and Enterprise Guard governance tiers in EUR. The surface is unusually machine-first: 16 OpenAPI 3.1 contracts, seven hosted MCP servers whose tools/list is open, an A2A agent card, llms.txt, an ai-plugin manifest, published JSON Schemas and ~40 vendor /.well-known/ manifests, all on a single host.

- Website: https://humanmirror.fr/
- Machine discovery: [llms.txt](https://humanmirror.fr/llms.txt) · [A2A agent card](https://humanmirror.fr/.well-known/agent-card.json) · [x402 OpenAPI](https://humanmirror.fr/x402/openapi.json) · [Nexus MCP](https://humanmirror.fr/api/nexus/mcp/)

## What this profile holds

| Area | Files | Method |
|---|---|---|
| `openapi/` | 16 first-party OpenAPI 3.1 contracts (verbatim JSON under `_original/`, YAML alongside) | searched |
| `mcp/` | 7 hosted MCP servers with live `tools/list` bodies (22 tools), 3 registry `server.json`, manifest + tool crosswalk | probed / derived |
| `a2a/` | Agent card at the canonical well-known path (graded flavored) + legacy `agent.json` | probed |
| `skills/` | Provider-published `skill.md` (verbatim) + 2 generated skills grounded in real operations | searched / generated |
| `json-schema/`, `json-ld/`, `postman/`, `llms/`, `well-known/` | Published schemas, JSON-LD index, 4 Postman collections, llms.txt, ai-plugin manifest | searched / probed |
| `conformance/`, `conventions/`, `errors/`, `lifecycle/`, `rate-limits/`, `plans/`, `sandbox/`, `cli/`, `packages/`, `regulatory/`, `security/`, `authentication/`, `overlays/` | Cross-cutting profiles derived from the contracts and the provider's own pages; a live x402 402 challenge is recorded in conformance | searched / derived / probed |

Everything under `openapi/_original/`, `mcp/*-tools.json`, `a2a/*.json`, `json-schema/`, `json-ld/`, `postman/`, `llms/` and `skills/*-genesis-skill.md` is the provider's document byte-for-byte; the `.yml` profiles say in their `method:` field how each was produced.
