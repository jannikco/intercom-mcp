# Intercom MCP server

Find support contacts and add a new lead contact without sending an outbound message.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `INTERCOM_ACCESS_TOKEN`



Credential help: https://developers.intercom.com/docs/build-an-integration/learn-more/authentication

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call intercom_list_contacts '{}'
```

## Use with an MCP client

Launch `node /absolute/path/intercom-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| intercom_list_contacts | Read | intercom list contacts |
| intercom_get_contact | Read | intercom get contact |
| intercom_create_contact | Explicit approval required | intercom create contact |

## Concrete workflow

Find support contacts and add a new lead contact without sending an outbound message.

1. intercom_list_contacts
2. intercom_get_contact
3. intercom_create_contact

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=intercom&integration=intercom-mcp&utm_source=github&utm_campaign=github-intercom-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/intercom/).

## Provenance and maintenance

- https://raw.githubusercontent.com/intercom/Intercom-OpenAPI/main/descriptions/2.15/api.intercom.io.yaml

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
