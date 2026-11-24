# StudyScout for Business MCP server

Order paid studies with US adults from your AI agent, and read the results: quick polls, surveys, video ad tests, ad rankings, recording sessions, AI interviews and usability tests. People come from StudyScout's panel of 130,000+ adults who signed up for paid studies.

This is a hosted remote server. There is nothing to install or run.

| | |
|---|---|
| Endpoint | `https://www.joinstudyscout.com/api/mcp` (Streamable HTTP) |
| Auth | `Authorization: Bearer <your API key>` |
| MCP Registry | `com.joinstudyscout/business` |

## Get an API key

A person makes one on the dashboard at [joinstudyscout.com/business](https://www.joinstudyscout.com/business/start). An agent with its own mailbox can get one alone: it signs in with the 6-digit code sent to that address, accepts the Business Terms for its company, then creates a key. The steps are under API in [llms.txt](https://www.joinstudyscout.com/llms.txt). A key is shown once.

## Connect

Claude Code:

```sh
claude mcp add --transport http studyscout https://www.joinstudyscout.com/api/mcp --header "Authorization: Bearer YOUR_KEY"
```

Cursor (`.cursor/mcp.json`) and other clients that take a URL and headers:

```json
{
  "mcpServers": {
    "studyscout": {
      "url": "https://www.joinstudyscout.com/api/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```

## Tools

One tool for each operation of the [StudyScout API](https://www.joinstudyscout.com/api/v1/openapi.json), named by its operationId:

- **Account:** `getAccount` (balance and what you pay per format), `countAudience` (how many members a targeting matches), `createTopUp` (a Stripe Checkout link to add funds)
- **Studies:** `createStudy`, `updateStudy`, `getStudy`, `listStudies`, `launchStudy`, `getStudyStatus`, `withdrawStudy`, `endStudy`, `deleteStudy`
- **Your own video, for an ad test:** `createUpload`, `completeUpload`
- **Results:** `getStudyResults`, `getStudyResultsSummary`, `getStudyResultsDetail`, `exportStudyCsv`, `listRecordings`, `getRecordingLinks`, `getMomentCommentLinks`, `listInterviews`, `getInterviewClipLinks`, `listUsabilitySessions`, `getUsabilitySessionLinks`

## What still takes a person

- Whoever holds the card pays the checkout link `createTopUp` returns, unless your agent can. No card details pass through the API.
- A person at StudyScout reviews every study before it goes to the panel. No key can approve one.

## Prices and terms

Prices are on [joinstudyscout.com/business](https://www.joinstudyscout.com/business#pricing), and `getAccount` returns what your account pays. You pay only for responses that pass our quality checks. See the [Business Terms](https://www.joinstudyscout.com/business/terms).

Questions: support@joinstudyscout.com
