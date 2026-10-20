---
inclusion: auto
name: soap-dry-run
description: Apply when implementing or testing SOAP integrations that could update menus or call live, shared, or external endpoints.
---

# SOAP Integration Dry-Run Safety

Use dry-run behavior by default when developing or testing a SOAP operation that changes menu data.

- Do not send the request to a live SDK, development, production, shared mock, or third-party callback
  endpoint such as `webhook.site`.
- Render the request and payload locally, or send them only to an approved local stub.
- Redact credentials, tokens, personal data, and internal identifiers from logs.
- Mark dry-run output clearly, for example with `SOAP_DRY_RUN=true`.
- Make an outbound call only when the user explicitly approves it and identifies the permitted target
  environment. Reconfirm before a destructive or production call.
