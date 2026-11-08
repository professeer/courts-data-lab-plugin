# Courts Data Lab plugin

This plugin connects Claude to Courts Data Lab, a read-only service for Indian court case data from Professeer. It covers the Supreme Court, the Bombay and Delhi High Courts, NCLT and NCLAT.

With the plugin, Claude can search cases by party or text, read a case's hearing history, and open the court orders. Its skills teach Claude to cite each case and order, to state what a search covers, and never to treat an empty search as proof.

## What you need

- Approved Courts Data Lab access and an API key. Access is by approval. See [Get access](https://api-docs.courtsdaily.info).
- Claude Code. Sign-in for Claude.ai, Claude Desktop and ChatGPT is coming. Until then, use a custom connector as the [connect guide](https://api-docs.courtsdaily.info/connect) explains.

## Install in Claude Code

```
claude plugin marketplace add professeer/courts-data-lab-plugin
claude plugin install courts-data-lab@courts-data-lab
```

Claude Code asks for your API key and keeps it in your system's secure credential store. Then try:

> Use Courts Data Lab to find CNR SCIN010499592024 and list its hearings with order links.

## Skills

| Skill | Use |
|---|---|
| `company-litigation-research` | Cases where a company or person is a party |
| `case-history` | Hearing history and orders of one case from its CNR |
| `coverage-check` | What the data covers, before any count or "no cases" answer |
| `search-syntax` | Quoted phrases, filters and paging |

## Limits

The service reads court records. It does not file cases, change records or send messages. Each distinct case returned counts towards your organisation's case allowance. A name match does not prove who a party is. Results are research material, not legal advice.

Support: https://api-docs.courtsdaily.info
