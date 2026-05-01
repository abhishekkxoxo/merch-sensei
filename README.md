# Claude Code Custom Commands

This directory contains custom slash commands for the Xoxoday project.

---

## 🗡️ `/merch-sensei` — Merchandise Vendor Integration Agent

Guides you through onboarding a new physical goods (merchandise) vendor into the Xoxoday platform end-to-end.

### What it does

1. **Accepts API docs** (Postman collection, OpenAPI JSON, or raw text) and pre-fills answers, or walks you through Q&A if you have nothing to paste.
2. **Asks 6 structured batches** of questions — vendor identity, auth, order placement, status tracking, product catalog, edge cases.
3. **Runs a feasibility check** and waits for your approval before writing anything.
4. **Confirms your Jira branch** before touching any file.
5. **Writes all required files automatically:**

| File | Action |
|------|--------|
| `vendor-integrations/src/vendors/integratedVendors/{VendorName}.ts` | Created |
| `vendor-integrations/src/vendors/vendorTemplates/{vendorName}Types.ts` | Created (if complex types needed) |
| `vendor-integrations/src/configs/vendorConfigs/{vendorId}_{vendorName}.json` | Created |
| `vendor-integrations/src/configs/config.json` | Updated (`vendorClassIdMapping` only) |

### What you still do manually after it finishes

1. Fill real credentials in `vendorConfigs/{vendorId}_{vendorName}.json` (replace `FILL_FROM_SECURE_CONFIG`)
2. Add vendorId to `order-process-ms/config_voucher_process.json` → `integratedVendors` array
3. Register webhook URL with the vendor (if applicable)
4. Run `cd vendor-integrations && npm run merge-configs && npx tsc`
5. Test order placement, webhook, and polling before going live

### Usage

```
/merch-sensei
```

Drop your vendor's API docs when prompted, or type `start` to begin Q&A.
