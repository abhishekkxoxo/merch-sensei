# MerchSensei 🗡️ — Merchandise Vendor Integration Agent

A Claude Code slash command for physical goods (merchandise) vendors on the Xoxoday platform. It has three modes:

| Mode | Use it to |
|---|---|
| **Onboard** | Integrate a new merchandise vendor: question batches → feasibility → branch check → code → tests → handoff |
| **Debug** | Diagnose order placement, webhook, status, tracking and product sync problems, hop by hop (read-only) |
| **Test** | Vendor API contract tests with the Postman CLI first, then Jest unit tests of our connector |

## What it writes

| File | Where | In the PR? |
|---|---|---|
| `src/vendors/integratedVendors/{ClassName}.ts` | vendor-integrations | Yes |
| `src/vendors/vendorTemplates/{vendorName}Types.ts` (if needed) | vendor-integrations | Yes |
| `src/configs/baseConfigs.json.sample` (`vendorClassIdMapping`) | vendor-integrations | Yes |
| `tests/vendors/{vendorName}.*.test.ts` + fixtures | vendor-integrations | Yes |
| `src/configs/vendorConfigs/{ClassName}.json` | vendor-integrations | No: gitignored, delivered per env via devx |

It never hand-edits `config.json`, which `npm run merge-configs` regenerates.

## What still needs doing outside this command

The handoff gives an ordered checklist covering:
- deployment config: VI vendor config and mappings, OPMS `vendorIntegration.integratedVendors` (string ids), and the plumAuth webhook routing (`api.integratedVendors`, `rawPayload`);
- the token, sync and polling schedulers;
- DB rows and tables;
- about 12 karma admin files;
- a staging smoke test.

Platform limits it flags up front:
- there is no outbound cancel;
- returns are not refunded;
- vendor-signed webhooks need escalation before building.

## Installation

```bash
cp merch-sensei.md /path/to/your/project/.claude/commands/
```

Then in Claude Code:

```
/merch-sensei
```

Drop your vendor's API docs, say `start`, or say `debug <vendor> <orderId|symptom>` or `test`.

## Related

- [akatsuki-gift-cards](https://github.com/abhishekkxoxo/akatsuki-gift-cards): gift card vendors
- [topup-sensei](https://github.com/abhishekkxoxo/topup-sensei): mobile topup / recharge vendors
