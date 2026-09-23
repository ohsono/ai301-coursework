# Rubric: is this a good first issue?

Four required checks, one per thing that kills a first contribution (repo
alive, nobody on it, scope fits, policy allows AI-assisted work), plus
four preferred checks that only rank accepted issues. Every threshold is
measured against the bundle's capture date in eval mode and against
today in live mode. Read "Reading the evidence" below before grading: it
fixes how each input format and each special case is read.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `repo-alive` | Repo facts: the `archived:` flag on the repo line, and the dates in "last 5 default-branch commits" (fallback: "last push to any branch"). Live: the archive banner and the default branch's commit history | Not archived, AND the newest qualifying commit (see R3) is dated within 180 days of the capture date. A missing release ("latest release: none published") does not fail this check | required |
| `not-claimed` | Repo facts line "this issue: assignees: ...; linked PRs: ..." plus every PR link or claim comment in the Comments section. Live: the Assignees and Development sidebar boxes and the thread | All four hold: (a) assignees is none; (b) no linked or thread-mentioned PR is `open`, including PRs from forks (`someone/repo#N`); (c) no human claim comment ("I'll take this", "working on this", "@zulipbot claim", "can I work on this") dated within 90 days of the capture date; (d) no maintainer comment reserving the issue for a named person or PR. Closed or merged PRs and claims older than 90 days with no open PR are stale and do not block | required |
| `bounded-scope` | The Issue section (title, opener line with association, labels, body) and the Comments section, plus closed linked PRs in repo facts. Live: the same on the issue page | The issue state is open, it asks for a code or docs change (not a usage question), and none of these holds: (a) it is an umbrella, tracking, or "megaissue" list, or asks to incrementally apply a change across the codebase; (b) two or more linked PRs are `closed` without merging (abandoned attempts); (c) it is a feature or enhancement request (not a bug report or a documentation change) that no maintainer (OWNER, MEMBER, or COLLABORATOR, bots excluded) opened or endorsed in the thread; (d) a maintainer says the design or approach still needs to be decided, or the body leaves a product decision open ("TBD", "confirm the intended design first"). A maintainer-filed bug whose body names its cause or causes counts as settled, even when it also lists optional extra ideas; (e) a maintainer says the fix needs core-internals changes; (f) three or more different people have claimed it (claim comments or bot claim commands) and none of their PRs merged | required |
| `ai-policy-allows` | Repo facts line "contribution policy ...". Live: CONTRIBUTING.md (root or `.github/`), docs it links to, and AI_POLICY-style files | Pass unless the policy bans AI-generated contributions outright (for example "We do not accept AI-generated code or documentation"). Conditions pass: disclosure, human review, personal understanding, testing, "fully AI-generated not accepted", or "closed if made with AI without human review". No policy, or no statement on AI, passes. An AGENTS.md file is a positive signal | required |
| `maintainer-responsive` | Repo facts "maintainer first-response sample", and maintainer comments in this thread | At least one sampled issue got a first maintainer reply within 14 days, or a maintainer commented in this thread within the last 365 days | preferred |
| `newcomer-label` | Labels on the opener line | A label matching "good first issue", "help wanted", "easy", or "beginner" (case-insensitive, ignoring emoji and punctuation) | preferred |
| `maintainer-filed` | Opener line association | Opened by OWNER, MEMBER, or COLLABORATOR (not a bot) | preferred |
| `fresh-issue` | Opener date vs capture date | Opened within 365 days of the capture date | preferred |

## Verdict rule

Accept if and only if all four `required` checks grade `pass`. Any
required `fail` or `unclear` rejects. Preferred checks never change the
verdict. They only rank accepted issues: more preferred passes rank
higher, and ties go to the fresher issue.

`unclear` is only for evidence that is genuinely absent after the
fallbacks in R1 to R6. Two checks treat silence as a pass:
`ai-policy-allows` (no statement means no restriction) and `not-claimed`
(no assignee, no PR, and no claim comment means unclaimed). Grade each
check on its own evidence. One check's failure never changes how another
is graded.

## Reading the evidence

**R1. Input formats.** Treat these as the same data:
- **Markdown bundle** (`issues/<id>.md`, what the harness sends): a
  metadata list (`source`, `captured`, `calibration`), then `## Repo facts`,
  `## Issue`, and `## Comments (N total, first M shown)`.
- **JSON twin** (`issues/<id>.json`): top-level `id`, `source`, `captured`,
  `calibration`, `issue`, `comments`, `comments_total`, `repo_facts`.
  `repo_facts` holds `raw_markdown` (the full repo-facts text), `assignees`
  (a list) and `linked_prs` (a list of `{ref, state}`). Each comment holds
  `author`, `author_association`, `date` and `body_markdown`.
- **Live mode**: `gh` or web output from the sources the evidence guide names.

Read fields by meaning, not position. If a structured field is missing,
null, empty, or shaped differently from the above (a string where a list
was expected, extra keys, different key order, a line reworded), fall
back to the same fact in `raw_markdown` or the markdown text, then to the
comment thread. Ignore keys you do not recognise. A formatting difference
alone never makes a check `unclear`.

**R2. Dates.** All dates are ISO `YYYY-MM-DD`. Compute day counts against
the `captured` date. When a bundle has two capture dates, use the one
stamped on that bundle. Commit and sample lists are not always
chronological, so use the maximum date in the list, not the first line.

**R3. Qualifying commits.** A commit counts toward `repo-alive` if a human
authored it, or if a bot merged a human's pull request ("Merge pull
request #N from <human>/..."). Commits that are only bot activity, such as
dependency bumps, pre-commit autoupdates, generated content or
leaderboards, do not count on their own. If the commit list is missing,
or contains no qualifying commit, fall back to "last push to any branch".

**R4. People.** Maintainer means OWNER, MEMBER, or COLLABORATOR. Some repos
(Zulip, for example) make every claimant a COLLABORATOR, so a COLLABORATOR
whose only comments are claims or "can I work on this" is a claimant, not
a maintainer. A maintainer answers, reviews, or decides. An
account whose name ends in `[bot]`, or that is plainly automation
(zulipbot, minikube-bot, kubernetes-prow, github-actions, cursor), is a
bot even when its association says MEMBER. Bot comments are never claims
and never maintainer endorsement. A human typing a bot command
("@zulipbot claim") is a claim by that human. A bot's stale or inactivity
notice neither clears nor makes a claim. CONTRIBUTOR, NONE,
FIRST_TIME_CONTRIBUTOR, FIRST_TIMER and MANNEQUIN are not maintainers.

**R5. The linked-PR line takes several shapes.** Handle each one:
- `none` means no linked PRs.
- `owner/repo#N (open|closed|merged)` entries are separated by `;`.
- `none formally linked (PR #N is referenced in the comment thread)`:
  find that PR in the thread and use the state stated there. If no state
  is stated and the reference is within 90 days of capture, treat it as
  open.

When the sidebar and the thread disagree, believe the thread.

**R6. Truncated or empty threads.** "(N total, first M shown)" with M < N
means later comments are hidden. Grade only what is shown, and never
assume what the hidden comments say. Because the hidden comments are the
newest ones, `not-claimed` cannot pass on silence when M < N: grade it
`unclear` unless a shown fact already fails it. "(no comments)" and "0 total" are
evidence of no claim, not missing evidence. An empty `description:` line
is not evidence of anything.

**R7. Unicode and encoding.** All input is UTF-8 text and every character
in it is valid content, including emoji (`✨`, `🙏`, `:sweat_smile:`),
smart quotes, en and em dashes, accented or non-Latin scripts, zero-width
characters, and HTML comments (`<!-- inactiveWarning -->`). Never stop,
error, or grade `unclear` because of an unusual character or a decoding
artefact (`â€™`, `’`, `�`). Read past it and use the surrounding
meaning. Match labels, keywords, and policy phrases case-insensitively,
after stripping emoji and punctuation.

**R8. Output hygiene.** The harness runs `json.loads` on the last fenced
JSON block. Keep each `evidence` value on one line. Escape any `"` and `\`
inside it, and replace backticks and newlines with plain text. Non-ASCII
characters may appear as-is (UTF-8) or as `\uXXXX` escapes; both are
valid. Use the check names exactly as written in the table. Grade every
check, preferred ones included, and emit exactly one fenced JSON block,
placed last.

## Special cases this rubric was calibrated on

These are the traps the eval set was built around, and how the checks
above resolve them:

- **Label without freedom.** A good-first-issue label does not mean the
  issue is free. An open linked PR, a fork PR, a recent claim comment, or
  a maintainer reserving the issue for someone fails `not-claimed`.
- **Stale claim with an invitation.** An old claim (older than 90 days),
  a closed attempt, and a maintainer saying "just give it a try" pass
  `not-claimed`. Age alone never fails an issue.
- **Alive without releases.** A repo with no releases but recent human
  commits passes `repo-alive`. A quiet repo with a few recent human
  commits also passes, and a thin response sample is only a preferred signal.
- **Dead despite a clean bug.** A newest qualifying commit more than 180
  days old, or an archived repo, fails `repo-alive` however good the issue text is.
- **Umbrella behind a friendly label.** A tracking list, a "megaissue",
  or "incrementally add X across the codebase" fails `bounded-scope`.
- **Debate history.** Two or more abandoned PRs, or an unresolved
  design discussion, fail `bounded-scope`.
- **Unendorsed wish.** A feature request opened by a bot or outsider with
  no maintainer response, especially one with "TBD" assets or product
  choices, fails `bounded-scope`. Bug and docs reports do not need
  endorsement.
- **Everything passes except policy.** An outright ban on AI-generated
  code or docs fails `ai-policy-allows` even when every other check passes.
