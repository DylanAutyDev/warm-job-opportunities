# Warm Job Opportunities

An Agent Skill for finding software engineering roles through warm leads and verified vacancies rather than cold applications.

Created by Dylan Auty. The skill started as a personal workflow that I ran on a schedule during my own job search. It is released in a personal capacity. The optional ATS Resume Checker mentioned below belongs to RemoteDevWork, a separate project of mine. I recommend it because I think it is a useful tool, not because of the connection.

## Why warm leads first

Warm introductions convert better than cold applications, and the gap is large.

Ashby analysed 38 million applications across 93,000 jobs between January 2021 and December 2024. About 40% of referred candidates moved from application to interview, against roughly 3% of inbound applicants. Referrals were about 1% of applications but a much larger share of hires. See [Ashby's referral report](https://www.ashbyhq.com/talent-trends-report/reports/referrals).

In my own search, warm leads converted to interviews at roughly 10 to 15%. Cold applications through an ATS converted at under 5%. That is one person's experience rather than a controlled study, and referral data carries some selection bias because people who get referrals often have an existing connection. The direction is consistent though. A short relevant message to a real decision-maker beats another anonymous application.

This skill is built around that difference. It spends most of its effort on finding live vacancies with a credible human contact, verifying that you can actually take the job and recording what you have already tried.

## What it does

- Builds a candidate profile from a CV and career preferences.
- Prioritizes international remote-first employers unless the candidate says otherwise.
- Matches real responsibilities and technical requirements, not just job titles.
- Verifies the employer, specific opening, remote arrangement, country eligibility and application route.
- Searches for warm opportunities from founders, CTOs and engineering leaders.
- Separates verified vacancies from outreach leads.
- Tracks applications, rejections, exclusions and feedback to avoid repeating opportunities.
- Supports mid-level through lead roles when they offer a credible fit and growth path.

## Requirements and compatibility

- Any agent that supports the open [Agent Skills specification](https://agentskills.io/specification).
- Web search or browser access. Search quality depends on the sources the agent can reach.
- File write access is recommended so the agent can maintain your CV, constraints and search history.
- No scripts, packages or build step. The skill is plain Markdown.

The skill continues to work without file access. In that case the agent returns updates that you can save yourself.

## Install

Clone the repository:

```bash
git clone https://github.com/DylanAutyDev/warm-job-opportunities.git
```

Then place the `warm-job-opportunities` folder in the skills directory that your agent supports. Most agents look in a personal directory such as `~/.claude/skills/` or a project directory such as `.opencode/skills/`. The exact location and activation method differ between agents, so check the agent's own documentation for Agent Skills support.

The folder name must match the `name` field in `SKILL.md`, so keep it as `warm-job-opportunities`.

## Get started

1. Open the skill in your AI agent.
2. Copy `assets/templates/cv.md` to `references/cv.md` and add your CV, or describe your experience in conversation.
3. Copy `assets/templates/constraints.md` to `references/constraints.md` and add your location, remote-work requirements, technical preferences and career goals.
4. Copy `assets/templates/search-history.md` to `references/search-history.md` to start your application log.
5. Ask the agent to find suitable opportunities.

You do not need to complete every reference file before starting. The skill can help you build them as you go, and it creates missing files from the templates when it can write to disk.

### CV help

A plain-text CV makes it easier for an agent to understand your experience and match you to real requirements.

If you need help extracting or reviewing your CV, RemoteDevWork offers a free [ATS Resume Checker and report](https://remotedevwork.com/ats-resume-checker). RemoteDevWork is a separate project of mine, so this is a direct recommendation rather than an independent review.

Using it is optional. You can also paste your CV into your AI agent or start with a summary of your experience.

## Running on a schedule

The skill works well as a recurring task. A weekly run keeps the search current and stops you from reapplying to roles you have already seen.

Modern AI solutions are adding scheduling as a first-class feature. Some desktop and chat apps run recurring tasks against a local folder, some agent harnesses support cron-style automations and others leave scheduling to the operating system. Feature names and limits change often, so check your tool's documentation for the current option. If your agent has a built-in scheduler, create a weekly job that opens this skill and runs a search.

Where built-in scheduling is unavailable, the same result comes from a local scheduler or a CI job. Windows Task Scheduler and cron can launch an agent CLI with a prompt, and GitHub Actions can run on a `schedule` trigger. The agent still needs web access and permission to write the reference files for the run to be useful.

A prompt that works well for a scheduled run:

```text
Use the warm-job-opportunities skill. Read my cv, constraints and search history.
Find up to three new verified vacancies and up to three warm outreach leads.
Exclude anything already in my pipeline. Update search-history.md and send me a
short digest with direct links and the verification date.
```

Two practical notes. Run the task during a period when you can respond to a warm lead, since replies lose value within a day or two. Keep the search history committed or backed up somewhere private so the exclusions survive a change of machine.

## Repository structure

```text
warm-job-opportunities/
├── README.md
├── SKILL.md
├── LICENSE
├── assets/
│   └── templates/
│       ├── cv.md
│       ├── constraints.md
│       └── search-history.md
└── references/
    └── methodology.md
```

- `SKILL.md` contains the agent instructions and the required frontmatter.
- `assets/templates/` holds blank templates for your personal files.
- `references/methodology.md` explains the research and verification standards.
- `references/cv.md`, `references/constraints.md` and `references/search-history.md` are created locally from the templates and are excluded by `.gitignore`.

## Privacy

Your CV, contact details, salary expectations and job-search history are personal information. Keep your populated reference files private.

The personal reference files are listed in `.gitignore` so they are not committed by accident. Before pushing changes to a public fork, check that you have not included personal information in any other file.

## Quality control

This skill is instructions, not software. It cannot verify anything by itself. The output is only as good as the harness it runs in and the model driving it.

The biggest variable is whether the agent can fetch the original source. A model that only reads search snippets will miss country restrictions, stale listings and the dates attached to hiring signals. The skill requires the agent to open the employer's careers page or official ATS, check that the application route works and record the verification date. If a page cannot be fetched, the agent should say so and you should treat that item as unverified.

Other things that affect quality:

- Model capability. Stronger tool use and longer context produce more reliable research.
- Tool availability. Browser, web search and file write access all change what the agent can confirm.
- Freshness. A check is only valid for the date recorded, which is why scheduled runs help.
- Prompt discipline. Limits such as three results and the exclusion rules hold better when you restate them.

A short checklist before trusting a result:

- Every vacancy has a direct link that opens.
- Country eligibility cites the employer's own words.
- Warm leads include a dated signal and a real contact route.
- Anything the agent could not fetch is labeled as unverified.

If a result looks thin, ask the agent which sources it opened and when. The answer is a quick signal of whether the harness did real research or only skimmed snippets.

## Limitations

The skill provides instructions, not a guaranteed job-search service. It does not independently create access to paid job boards, private communities or social networks. The agent must have suitable tools and access to current sources.

A vacancy page can remain online after hiring has slowed or stopped. The skill requires the agent to distinguish a live page from confirmed active hiring and to explain uncertainty.

Conversion rates vary by market, seniority and skill set. Treat the figures above as context rather than a forecast.

## Contributing

Improvements to the matching process, verification standards, reference templates and portability are welcome. Keep the instructions practical, tool-neutral and aligned with the Agent Skills specification.

## License

MIT. See [LICENSE](LICENSE).
