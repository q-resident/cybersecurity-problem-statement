## Recommended project

### Problem statement

**“Build a mini Security Operations case study: detect suspicious activity in authentication and system logs, rate the risk, and recommend controls using a standard framework (NIST CSF / CIA triad).”**

A small fictional company gives you 1–2 weeks of login and system logs. Your job is to:

1. Identify likely attack patterns (brute force, credential stuffing, privilege misuse, anomalous logins).
2. Classify findings by severity and impact.
3. Map each finding to a control/recommendation (access control, MFA, logging, least privilege, patching, etc.).
4. Deliver a short incident-style report a hiring manager can skim in 5 minutes.

That hits **Course 1** (attacks/tools), **Course 2** (OS/user admin thinking), **Course 3** (risk + frameworks), and optionally **Course 4** if you add a tiny DB permissions/SQL-injection appendix.

---

## Dataset (keep it simple)

Use a **public, labeled or semi-realistic log dataset**, not production data:

| Option | Why it works | Difficulty |
|--------|----------------|------------|
| [AIT Log Dataset](https://zenodo.org/records/7119953) (auth/system logs) | Realistic enterprise-style logs | Medium |
| [Honeypot / auth failure logs on Kaggle](https://www.kaggle.com/datasets) (search “SSH logs”, “failed login”) | Easy to analyze with Python/pandas | Easy |
| [CIC-IDS / UNSW-NB15](https://www.unsw.adfa.edu.au/unsw-canberra-cyber/cybersecurity/ADFA-NB15-Datasets/) | Classic network IDS datasets | Harder — only if you want network focus |

**Best starter choice:** a small **SSH / failed-login / authentication log** dataset (CSV or syslog). Easier to explain in interviews than a full IDS feature dump.

If public data feels heavy, you can also **generate synthetic logs** (Python script that writes normal + attack traffic) and document how they were generated — that still looks intentional and honest.

---

## What the GitHub repo should contain

Keep the repo **small and polished**:

```
cyber-log-threat-assessment/
├── README.md                 # problem, method, findings, how to run
├── data/                     # sample logs (or link + download script)
├── notebooks/ or scripts/    # analysis (pandas + simple rules)
├── findings/
│   ├── risk-register.md      # findings table: ID, severity, evidence, control
│   └── sample-alerts.md      # 3–5 example alerts with explanation
├── report/
│   └── security-assessment.pdf or .md
└── docs/
    ├── methodology.md        # CIA triad + NIST mapping
    └── controls-checklist.md # recommended remediations
```

**Impressive but simple analysis (rules, not ML):**
- >N failed logins from one IP in M minutes → brute force
- Success after many failures → possible credential compromise
- Login outside business hours / new geo (if fields exist)
- Same user, many hosts → lateral-movement hint
- Privileged account anomalies

No need for fancy ML. Interviewers care more that you can **explain evidence → risk → control**.

---

## README story you should tell

1. **Context:** “Junior analyst exercise for Acme Corp after suspicious login spikes.”
2. **Scope:** auth/system logs only; no live hacking.
3. **Method:** parse logs → detection rules → triage → risk rating → map to NIST CSF Identify/Protect/Detect/Respond.
4. **Findings:** 4–6 concrete findings with severity (Critical/High/Medium).
5. **Recommendations:** MFA, lockout policy, centralized logging, least privilege, monitoring playbook.
6. **Ethics note:** educational / defensive only; dataset is public or synthetic.

That README *is* the authenticity proof.

---

## Why this works for internships

- Matches entry roles: **SOC analyst / junior security analyst / GRC junior**.
- Shows you can turn course theory into a **repeatable security process**.
- Easy to demo live: “Here’s an alert, here’s why it matters, here’s the fix.”
- Avoids red-team/exploit repos that look risky or overclaim skills you don’t have yet.

---

## Two solid backups (if you prefer another angle)

**A. OWASP + DB security mini-lab (Course 4 heavy)**  
Tiny vulnerable vs secure login/query demo, SQL injection prevented with parameterized queries, role/permission matrix, short write-up mapped to OWASP Top 10.  
*Best if you like hands-on coding more than log analysis.*

**B. Compliance gap assessment (Course 3 heavy)**  
Fictional company profile → checklist against NIST CSF or ISO 27001-style controls → gap report + 30/60/90-day remediation plan. Less code, more writing — good for GRC/compliance internships.

---

## Suggestions

Ship **one repo in 1–2 weeks**: *Log-based Threat Detection & Risk Assessment*, using a public auth-log dataset, with a clean risk register and NIST-mapped recommendations. That is enough authenticity for the next phase without pretending he’s a penetration tester.
