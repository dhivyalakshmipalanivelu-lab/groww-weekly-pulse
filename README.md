# Groww Weekly Product Pulse (review insights to support explainer)

n8n workflow that turns 12 weeks of Google Play reviews of the Groww app (617 reviews, 20 Jul to 19 Sep 2026) into an internal weekly pulse and a support-ready fee explainer, then logs both to a Google Doc and creates a Gmail draft after human approval.

## How to run
1. Import workflows/groww-mcp-server.json and workflows/groww-pulse-agent.json into n8n.
2. Add credentials: Google (Sheets, Docs, Gmail) and OpenAI.
3. Upload data/groww_reviews_12wk_raw.csv to a Google Sheet and select it in the Google Sheets node.
4. In the server workflow, set your log Doc ID and your email in the two tools, activate it, and copy its production URL into the MCP client in the agent workflow.
5. Send "run the weekly pulse" in the n8n chat.

## Where MCP approval happens
The agent's two MCP tools (append to Google Doc, create Gmail draft) each sit behind a human review step (Gmail "Send and Wait for Response"). The agent pauses and emails an Approve/Decline request showing the tool name and content. Declining writes nothing. No tool can send email.

## Fee issue identified from reviews
Users cannot tell what makes up the total deducted on a trade beyond the quoted brokerage (STT, stamp duty, GST, exchange, SEBI and DP charges). 70 of 617 reviews (about 11%) mention a fee; 52 are 1-star. Typical complaint: "I donot know what kind of external charges and tax they are taking."

## Limits
- Sample is half 1-star, half 5-star, so it skews negative.
- Data ends 19 Sep 2026.
- NSE page text was pasted manually because automated access was blocked.
- Theme counts vary by a few reviews between runs (an LLM tags them).
