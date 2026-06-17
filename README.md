# Traceline — Requirement → Test Case Automation

A small browser-based tool that takes raw requirement text (BRD / FRD / user story / acceptance criteria) and automatically drafts structured test cases — positive, negative, boundary, and security scenarios — with priority, preconditions, steps, and expected results. Built as a working demonstration of automating a repetitive BA/QA handoff task that is normally done manually line by line.

## Why this exists

As a Business Analyst, a recurring bottleneck is the gap between "requirement is signed off" and "QA has a usable test case list." That translation is mechanical enough to automate: most requirements already signal their own test scenarios through specific words — "must / shall" signals priority, "maximum / minimum / limit" signals a boundary case, "password / login / OTP" signals a security case, and so on. Traceline encodes that pattern-matching so the first draft of a test suite exists in seconds instead of an hour of manual write-up, leaving the analyst to review and refine rather than start from a blank sheet.

## How it works

1. Paste requirement text into the intake box (numbered lists, bullet lists, or plain paragraphs all work).
2. The parser splits the text into individual requirement statements.
3. Each statement is scanned for keyword patterns and numeric limits to decide which test types apply.
4. A ledger of test cases is rendered, grouped by requirement, each with an ID, type, priority, precondition, steps, and expected result.
5. Export the full set to CSV for import into a tracker (Jira, Azure DevOps, Excel).

This is a **rule-based NLP heuristic engine** — it runs entirely in the browser, needs no API key, and works offline. There is an optional second step that calls the Claude API (using a key you supply at runtime, never stored or committed) to suggest one additional edge case per requirement on top of the rule-based list. That step is a bonus, not a dependency — the core tool stands on its own.

## Tech stack

Vanilla HTML, CSS, and JavaScript. No build step, no framework, no backend. Deployable as-is to GitHub Pages.

## Run it locally

Clone the repo and open `index.html` directly in a browser, or serve it:

```
git clone <your-repo-url>
cd traceline
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deploy to GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Set source to the `main` branch, root folder.
4. Your live link will be `https://<username>.github.io/<repo-name>/`.

## Possible next steps

- Export directly to Jira/Azure DevOps via their REST APIs instead of CSV.
- Accept BRD uploads (.docx/.pdf) instead of pasted text.
- Replace the rule-based core with an LLM-backed parser for more nuanced edge-case detection while keeping the rule engine as an offline fallback.

## Author

Gaurav Srivastava — Senior Business Analyst, MES/Manufacturing domain.
