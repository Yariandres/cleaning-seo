# cleaning-seo

SEO desk for the mobile cleaning business in Poznań. A **seo-specialist** agent researches searches, writes page briefs for the designer, sets technical requirements for the developer, audits staging, plans Google Business Profile, and reports after launch.

## Start

```bash
git clone https://github.com/Yariandres/cleaning-seo.git
cd cleaning-seo
claude
```

Then, for example: *"Use the seo-specialist agent. Validate the keyword seeds and write the SEO brief for the stroller counter."*

## The loop

```
SEO brief ──► Designer ──► tagged handover ──► Developer ──► "Ready for SEO review" ──► SEO audit ──► "SEO fix" ──► Developer
```

| Path | What |
|---|---|
| `.claude/agents/seo-specialist.md` | The agent, incl. the local SEO playbook |
| `.claude/skills/` | seo-audit, programmatic-seo, ai-seo (pinned in `skills-lock.json`) |
| `seo/strategy.md` | Strategy and keyword seeds |
| `seo/keywords/` | Keyword map |
| `seo/briefs/` | Page briefs (template: `_template.md`) |
| `seo/audits/` | Staging/production audits |
| `seo/gbp/` | Google Business Profile plan and posts |
| `seo/reports/` | Monthly reports after launch |
| `docs/prd.md`, `docs/source/` | Product requirements and research |
