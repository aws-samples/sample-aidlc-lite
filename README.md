# AI-DLC Lite — Personal Edition

A personal, Claude-focused variant of [AI-DLC Lite](https://github.com/aws-samples/sample-aidlc-lite), the lightweight version of the [AI-Driven Development Life Cycle](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) workflow.

This repo strips the multi-tool setup (Kiro, Amazon Q, Cursor, Cline, Copilot) down to the Claude Code path only, and trims docs to match. The underlying rules and three-phase workflow are unchanged from upstream.

> [!IMPORTANT]
> Generative AI can make mistakes. Review all output and costs from your AI model and coding assistant. See [AWS Responsible AI Policy](https://aws.amazon.com/ai/responsible-ai/policy/).

## What is AI-DLC Lite?

A structured three-phase workflow (Inception → Construction → Operations) with approval gates, audit logging, and state tracking — optimized for speed over exhaustive analysis. Compared to full AI-DLC: fewer questions, one follow-up round, single approval per stage, inline clarifications.

For the full methodology, see the [blog post](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) and the [Method Definition Paper](https://prod.d13rzhkk8cj2z0.amplifyapp.com/). For the change list vs. full AI-DLC, see [`aidlc-rules/aws-aidlc-lite-rule-details/LITE-CHANGES.md`](aidlc-rules/aws-aidlc-lite-rule-details/LITE-CHANGES.md).

---

## Quick Start (Claude Code)

Clone this repo:
```bash
git clone git@github.com:CodingDevotion/aidlc-lite.git
```

Create your project folder as a sibling to the cloned repo:
```bash
mkdir <my-project>
cd <my-project>
```

Install the rules into the project. Pick one of the two layouts:

### Option 1 — Project root (recommended)
```bash
cp ../aidlc-lite/aidlc-rules/aws-aidlc-lite-rules/lite-core-workflow.md ./CLAUDE.md
mkdir -p .aidlc-lite-rule-details
cp -R ../aidlc-lite/aidlc-rules/aws-aidlc-lite-rule-details/* .aidlc-lite-rule-details/
```

Resulting layout:
```
<my-project>/
├── CLAUDE.md
└── .aidlc-lite-rule-details/
    ├── common/
    ├── inception/
    ├── construction/
    └── operations/
```

### Option 2 — `.claude/` directory
```bash
mkdir -p .claude
cp ../aidlc-lite/aidlc-rules/aws-aidlc-lite-rules/lite-core-workflow.md .claude/CLAUDE.md
mkdir -p .aidlc-lite-rule-details
cp -R ../aidlc-lite/aidlc-rules/aws-aidlc-lite-rule-details/* .aidlc-lite-rule-details/
```

### Verify
1. Start Claude Code in your project directory (`claude` CLI or VS Code extension).
2. Run `/config` or ask: "What instructions are currently active in this project?"

---

## Usage

1. Start a project by saying **"Using AI-DLC, ..."** in chat.
2. The workflow activates automatically.
3. Answer the targeted questions.
4. Review the execution plan.
5. Approve each stage's artifacts.
6. Generated artifacts land in `aidlc-docs/`.

### Three phases
- **Inception** — what to build and why (requirements, user stories, application design).
- **Construction** — how to build it (functional/NFR design, code generation, build/test).
- **Operations** — deploy and monitor (future).

---

## Extensions

Layered rules under `aidlc-rules/aws-aidlc-lite-rule-details/extensions/`, grouped by category (e.g., `security/`, `testing/`). Each extension has a rules file and an opt-in prompt presented during Requirements Analysis. Built-in: `security/baseline/` and `testing/property-based/`.

To add your own: create `extensions/<category>/<name>/`, add a `<name>.md` rules file with `## Rule <PREFIX-NN>: <Title>` headings, and a `<name>.opt-in.md` prompt (omit the opt-in file to make the extension always-on).

> [!IMPORTANT]
> The bundled security extension is directional reference material. Build, customize, and test your own security rules before relying on them in production.

---

## Git remotes

This repo is wired to three remotes — different jobs for each.

```
origin           git@github.com:CodingDevotion/aidlc-lite.git           (this private repo)
upstream         git@github.com:aws-samples/sample-aidlc-lite.git       (where AI-DLC Lite is maintained)
upstream-fork    git@github.com:CodingDevotion/sample-aidlc-lite.git    (old public fork — PR launchpad)
```

- **`origin`** — your private repo. `git push` and `git pull` default here.
- **`upstream`** — the repo where the **Lite** variant of AI-DLC is maintained (published under `aws-samples`). Note: this is *not* the canonical source of AI-DLC as a whole — the full AI-DLC methodology lives in the [blog post](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) and the [Method Definition Paper](https://prod.d13rzhkk8cj2z0.amplifyapp.com/). This remote is read-only; use it to pull in updates the maintainers make to the Lite rules.
- **`upstream-fork`** — my original public fork, kept around solely as a launchpad for contributing changes back to the AWS Lite repo if I ever want to.

### Pull the latest from AWS Lite repo
```bash
git fetch upstream
git merge upstream/main          # or: git rebase upstream/main
```
Resolve any conflicts (most likely in `README.md` or files you've customized), then `git push origin main`.

### Contribute a change back to from AWS Lite repo
Private repos can't open PRs to public ones, so route contributions through `upstream-fork`:
```bash
git push upstream-fork <branch-name>
```
Then open the PR on GitHub from `CodingDevotion/sample-aidlc-lite` → `aws-samples/sample-aidlc-lite`.

### Recreate this remote setup from a fresh clone
```bash
git clone git@github.com:CodingDevotion/aidlc-lite.git
cd aidlc-lite
git remote add upstream      git@github.com:aws-samples/sample-aidlc-lite.git
git remote add upstream-fork git@github.com:CodingDevotion/sample-aidlc-lite.git
```

---

## Version control recommendations

Commit to your project repo:
```
CLAUDE.md
.aidlc-lite-rule-details/
```

Optionally gitignore:
```
.claude/settings.local.json
```

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Rules not loading | Verify `CLAUDE.md` (or `.claude/CLAUDE.md`) exists at the project root |
| Rule details not found | Verify `.aidlc-lite-rule-details/` exists with its subdirectories |
| Changes not picked up | Start a new Claude Code session |
| Encoding issues | Ensure files are UTF-8 |
| Windows paths | Use forward slashes inside markdown content |

Claude Code specifics: `/config` to view config; ask "What instructions are currently active?" to confirm rules are loaded.

---

## Generated artifacts

For the full reference of files produced by the workflow, see [docs/GENERATED_DOCS_REFERENCE.md](docs/GENERATED_DOCS_REFERENCE.md).

---

## Resources

| | |
|---|---|
| Upstream repo | [aws-samples/sample-aidlc-lite](https://github.com/aws-samples/sample-aidlc-lite) |
| AI-DLC Method Definition Paper | https://prod.d13rzhkk8cj2z0.amplifyapp.com/ |
| AI-DLC blog | https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/ |
| Open-sourcing AI-DLC blog | https://aws.amazon.com/blogs/devops/open-sourcing-adaptive-workflows-for-ai-driven-development-life-cycle-ai-dlc/ |
| Walkthrough blog | https://aws.amazon.com/blogs/devops/building-with-ai-dlc-using-amazon-q-developer/ |
| Claude Code | https://github.com/anthropics/claude-code |
| Working with AI-DLC | [docs/WORKING-WITH-AIDLC.md](docs/WORKING-WITH-AIDLC.md) |

---

## License

Upstream is licensed under MIT-0. See [LICENSE](LICENSE).
