# Next Task

## Goal

Add recovery Telegram notification when status changes from DOWN → UP.

## Verify

1. Import `monitoring/website-uptime-monitor/workflow.json` into n8n.
2. Configure Sheet ID, Chat ID, credentials, and website URL.
3. Create Checks + Latest Status sheets with required columns.
4. Test with an invalid URL → expect DOWN alert once.
5. Restore a valid URL → currently no recovery alert (next feature).
