# Support Ticket Analysis Skill

## Purpose
Use this skill when working on the ShopNest Global support ticket intelligence proof of concept. This project analyzes a CSV-based support-ticket data dump and turns noisy, unstructured customer messages into structured summaries and response drafts.

## Dataset Snapshot
The project data source is the file `support_ticket_data.csv` in this folder. The real schema in the dataset is:
- `support_ticket_id`: integer identifier for each ticket
- `support_ticket_desc`: raw customer issue text

This dataset contains a wide mix of support requests, including:
- delivery delays and missing packages
- wrong item or damaged item delivery
- refund and return requests
- payment failure or duplicate charge issues
- order cancellation and stock/inventory mismatch complaints
- address update requests
- general status-check or follow-up questions
- escalation and complaint-style messages from frustrated customers

## Business Context
ShopNest Global operates a large-scale e-commerce platform across many geographies and serves millions of customers. Customers contact support with tickets that are often inconsistent, emotionally charged, and missing key details.

The company needs a low-code AI workflow to help support agents quickly understand the real issue, draft a prompt-quality response, and reduce the effort spent on manual ticket decoding.

## Project Objective
Build an AI-powered support ticket analysis POC that:
1. reads raw support ticket descriptions,
2. extracts the real issue in a clear summary,
3. scores the summary with an LLM-as-Judge approach,
4. generates a professional and empathetic response,
5. evaluates the response quality,
6. and exports the final outputs into a structured table.

## What the Model Should Learn from the Data
The dataset shows that tickets do not always follow a clean format. They may contain:
- order IDs and product names embedded inside a complaint
- incomplete or vague references
- informal language, slang, or abbreviated text
- emotional or urgent customer language
- duplicate or contradictory information

The goal is not to preserve the tone exactly, but to extract the underlying intent and produce a clear support-ready interpretation.

## Expected Solution Flow
The ideal workflow for this project is:
1. Load the CSV file.
2. Read each row using `support_ticket_id` and `support_ticket_desc`.
3. Generate a concise summary of the issue.
4. Evaluate whether the summary is complete, accurate, and useful.
5. Generate a customer response that is empathetic, polite, and policy-aware.
6. Evaluate the response quality.
7. Store everything in a final structured output table for downstream analysis.

## Output Expectations
Each processed ticket should result in a structured row containing:
- ticket ID
- original ticket description
- summarized issue
- summary quality score
- generated response
- response quality score
- final exported output record

## Prompting Guidance
When writing prompts for this project:
- summarize the issue neutrally and factually
- identify the requested action: refund, replacement, return, status check, cancellation, billing clarification, or delivery follow-up
- preserve important operational details such as order numbers, product names, and urgency
- do not overfit to the emotional tone; convert it into a clean support summary
- generate responses that are empathetic, professional, and aligned to support policy

## Solution Design Principles
- Keep the pipeline explainable and auditable.
- Treat the data dump as unstructured real-world support text.
- Focus on customer intent extraction rather than raw text copying.
- Prioritize consistency across all tickets.
- Use the project as a proof of concept for AI-assisted support operations.

## Success Criteria
The project is successful if it can demonstrate that:
- noisy ticket descriptions can be mapped into a structured issue summary,
- AI-generated responses are relevant and professional,
- evaluation methods can score output quality consistently,
- and the final results can be exported into one clean table for reuse.

## Developer Notes
When extending this project:
- keep `support_ticket_id` intact in every final output row,
- make the summary concise but not incomplete,
- ensure the final response is grounded in business policy and customer empathy,
- and export the final combined results in one table for downstream workflow automation or reporting.

## Model Selection Note
For this project, the selected model is a hosted LLM API such as OpenAI `gpt-4.1-mini` or `gpt-4o-mini`.

We chose this because the task is not only to classify tickets, but also to summarize messy text, draft helpful customer responses, and evaluate the quality of both outputs. A hosted instruction-following model gives the best balance of quality, speed, and ease of use for a notebook-based proof of concept.

In simple terms: this model is the best fit because it can understand noisy support messages, follow instructions well, and generate professional responses that are suitable for a real support workflow.

## Temperature Note
A temperature of `0.2` is selected for this project.

This is intentional because the required behavior is to summarize incoming raw, unstructured tickets into a clean, concise summary for the support agent. A low temperature reduces creativity, keeps the output more stable, and helps the model stay focused on factual extraction instead of producing overly imaginative or verbose text.
