# devops-error-fixer
An automated SRE triage pipeline that ingests production stack traces via webhooks, uses Gemini for root-cause diagnosis, and generates structured debug cards.
# Self-Healing DevOps Error Logger

An automated, self-healing Site Reliability Engineering (SRE) triage pipeline. It securely captures live application crashes, parses raw stack traces, runs them through AI diagnostics for root-cause analysis, and logs actionable debug resolutions to minimize Mean Time to Resolution (MTTR).

## 🚀 How It Works
1. **Incident Trigger:** Production runtime environments post real-time error logs and stack traces directly to a dedicated n8n Webhook.
2. **Stack Trace Parsing:** Filters out environment noise to isolate specific file names, line numbers, programming languages, and exception messages.
3. **AI Root-Cause Diagnosis:** Passes the isolated crash details to a Google Gemini model, which analyzes the trace, identifies the logical bug, and writes a fully drafted code fix.
4. **Automated Ticketing & Alerts:** Generates structured developer cards on tracking boards and pushes instant, actionable diagnostic alerts to Slack channels with the proposed solution.

## 🛠️ Tech Stack & Integrations
* **Workflow Orchestration:** n8n
* **Diagnostic LLM Core:** Google Gemini Model
* **Incident Ingestion:** HTTP/1.1 REST Webhook Handlers
* **Engineering Tools:** GitHub Issue API, Developer Notification Channels (Slack/Discord)

## 📋 Sample Monitored Input (POST Payload)
```json
{
  "service_name": "payment-gateway-service",
  "environment": "production",
  "error_message": "NullPointerException: Cannot invoke \"String.toLowerCase()\" because \"status\" is null",
  "stack_trace": "Exception in thread \"main\" java.lang.NullPointerException...\n\tat com.project.payments.PaymentProcessor.verifyTransaction(PaymentProcessor.java:42)"
}
