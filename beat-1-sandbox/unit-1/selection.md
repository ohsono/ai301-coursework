# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72

**Verdict output**

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

Live run of 2026-09-23 on three candidates (#72, #69, #68). Command:
`claude -p --model sonnet "issue-select: grade these candidate first issues: <#72> <#69> <#68>"`.
The skill accepted all three and ranked #72 first. #72's verdict is the first object in the JSON array.

````text
## Summary — Path Review candidates, all three **accept**

All three are seeded bugs opened by the same COLLABORATOR (Aburke225) on 2026-09-10, all `bug` + `good first issue`, all pass every required check. Ranked by fit to your Trustworthy AI / guardrails background:

1. **#72 — `verify_password` raises instead of failing closed** ([issue](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72)) — a fail-open auth bug: exactly the security/guardrail territory your profile names. Only 1 classroom claimant so far.
2. **#69 — output parser crashes on a top-level JSON array** ([issue](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69)) — LLM output robustness, close second fit for agentic-harness work. 3 students have posted "I'd like to work on this" with zero PRs open — see tension note below.
3. **#68 — keyword search `ZeroDivisionError` on empty index** ([issue](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68)) — solid bounded bug, least directly tied to your stated interests. 1 classroom claimant.

All three tie on preferred checks (label pass, maintainer-filed pass, fresh pass, maintainer-responsive fail — sampled 5 other recently-updated issues, no OWNER/MEMBER/COLLABORATOR reply found anywhere in this repo). Freshness tie-break (by opener timestamp, seconds apart) happens to agree with the fit ordering above.

**Rubric tension worth fixing on #69:** `bounded-scope` condition (f) ("three or more different people have claimed it... none of their PRs merged") reads literally against #69 — 3 claim comments, 0 PRs. I graded it `pass` per the scope.md house rule ("there may be several [claims] on one issue... is normal. Claim anyway"), since SKILL.md says a house rule governs *any* check that reads claim comments as evidence, not just `not-claimed`. But (f) was written for a different signal — repeated failed real-world attempts — and a classroom of same-day interest comments with zero PRs doesn't carry that signal. Consider tightening (f) to require at least one opened PR before it can fire, so it doesn't accidentally target popular classroom issues.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "not archived; newest default-branch commit by human Aburke225 on 2026-09-16, 7 days before today"},
      {"name": "not-claimed", "grade": "pass", "evidence": "no assignees, no linked/open PRs (gh pr list search for 68/69/72 returned empty); one NONE-association claim comment, ignored per scope.md house rule"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "open bug filed by COLLABORATOR Aburke225 naming the exact cause (UnknownHashError escaping verify_password), single-file fix, no core-internals statement, no abandoned PRs"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no statement on AI-generated contributions; silence passes"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "sampled 5 recently-updated issues (#53,#67,#60,#57,#62): no OWNER/MEMBER/COLLABORATOR comment in any"},
      {"name": "newcomer-label", "grade": "pass", "evidence": "labels include good first issue"},
      {"name": "maintainer-filed", "grade": "pass", "evidence": "opener Aburke225 has author_association COLLABORATOR"},
      {"name": "fresh-issue", "grade": "pass", "evidence": "opened 2026-09-10, 13 days before today"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "not archived; newest default-branch commit by human Aburke225 on 2026-09-16, 7 days before today"},
      {"name": "not-claimed", "grade": "pass", "evidence": "no assignees, no linked/open PRs (gh pr list search returned empty); three NONE-association claim comments, ignored per scope.md house rule"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "open bug filed by COLLABORATOR Aburke225 naming the exact cause (.items() on a list), single-file fix; condition (f) reads literally (3 claimants, 0 PRs merged) but is treated as classroom-normal per scope.md house rule since none of the three same-week comments reflect an abandoned real attempt (0 PRs opened by any of them)"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no statement on AI-generated contributions; silence passes"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "sampled 5 recently-updated issues (#53,#67,#60,#57,#62): no OWNER/MEMBER/COLLABORATOR comment in any"},
      {"name": "newcomer-label", "grade": "pass", "evidence": "labels include good first issue"},
      {"name": "maintainer-filed", "grade": "pass", "evidence": "opener Aburke225 has author_association COLLABORATOR"},
      {"name": "fresh-issue", "grade": "pass", "evidence": "opened 2026-09-10, 13 days before today"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "not archived; newest default-branch commit by human Aburke225 on 2026-09-16, 7 days before today"},
      {"name": "not-claimed", "grade": "pass", "evidence": "no assignees, no linked/open PRs (gh pr list search returned empty); one NONE-association claim comment, ignored per scope.md house rule"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "open bug filed by COLLABORATOR Aburke225 naming the exact cause (BM25Okapi ZeroDivisionError on empty corpus), single-file fix, no abandoned PRs"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no statement on AI-generated contributions; silence passes"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "sampled 5 recently-updated issues (#53,#67,#60,#57,#62): no OWNER/MEMBER/COLLABORATOR comment in any"},
      {"name": "newcomer-label", "grade": "pass", "evidence": "labels include good first issue"},
      {"name": "maintainer-filed", "grade": "pass", "evidence": "opener Aburke225 has author_association COLLABORATOR"},
      {"name": "fresh-issue", "grade": "pass", "evidence": "opened 2026-09-10, 13 days before today"}
    ],
    "verdict": "accept"
  }
]
```
````

The run printed a "Next steps" block after the JSON block, which is left out above. It suggested
posting a claim comment, which I did not do: claiming is Unit 2's work.

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Partial run, `--only issue-01,issue-14,issue-19,issue-12,issue-09,issue-15` (the six hardest
   items): **6/6**.
2. Partial run, `--only issue-12,issue-15 --out`, to see which check rejected each: **2/2**.
   issue-12 failed only `ai-policy-allows`; issue-15 failed only `bounded-scope`.
3. Full run, rubric sha256 `8f3a03b43f843508`: **19/20** (bar: 18/20: PASS). Categories:
   `claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 1/1  scope 4/4`. The miss was
   `issue-04  accept  reject   NO     failed: bounded-scope`.
4. Rubric revised (clause (f) in `bounded-scope`, R4, R6). Partial run,
   `--only issue-15,issue-09,issue-08,issue-18,issue-12`: **5/5**.
5. Full run, rubric sha256 `6e04ec132112bbc8`, the committed `eval-run.txt`:
   `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Issue analysis**

issue-04 (zxcalc/zxlive#555). Gold label: `accept`. My rubric's decision in the committed
run: `accept`. In run 3 it was `reject`.

The bundle's issue body is one line: "Including remove identity, fuse spiders, remove self
loops, etc." It was "opened by RazinShaikh (COLLABORATOR) on 2026-08-04" with "labels: Type: bug,
good first issue", and has "(no comments)". In the final run every required check passed:
- `repo-alive`: "newest qualifying commit 2026-08-04, 1 day before capture 2026-08-05".
- `not-claimed`: "assignees: none; linked PRs: none; 0 total comments".
- `bounded-scope`: "open bug filed by COLLABORATOR RazinShaikh naming its causes (remove
  identity, fuse spiders, remove self loops)".
- `ai-policy-allows`: "no statement on AI or contribution tooling".

In run 3 the same rubric failed it on `bounded-scope`. My reading is that the list with "etc."
looked like clause (a), "an umbrella, tracking, or 'megaissue' list". I can't confirm that:
run 3's per-check evidence was overwritten by run 5's `--out` file, and only the
`failed: bounded-scope` note survives in the earlier commit. None of the revisions between runs
3 and 5 targeted this issue, so the flip is grader variance on a borderline one-line body, not
a fix. It is the item I would watch first if a later run drops below the bar.

**Check rationale**

`not-claimed`, with the reading rule R6 that governs it, as currently written in
`tools/issue-select/rubric.md`:

> | `not-claimed` | Repo facts line "this issue: assignees: ...; linked PRs: ..." plus every PR link or claim comment in the Comments section. Live: the Assignees and Development sidebar boxes and the thread | All four hold: (a) assignees is none; (b) no linked or thread-mentioned PR is `open`, including PRs from forks (`someone/repo#N`); (c) no human claim comment ("I'll take this", "working on this", "@zulipbot claim", "can I work on this") dated within 90 days of the capture date; (d) no maintainer comment reserving the issue for a named person or PR. Closed or merged PRs and claims older than 90 days with no open PR are stale and do not block | required |

> **R6. Truncated or empty threads.** "(N total, first M shown)" with M < N means later comments are hidden. Grade only what is shown, and never assume what the hidden comments say. Because the hidden comments are the newest ones, `not-claimed` cannot pass on silence when M < N: grade it `unclear` unless a shown fact already fails it. "(no comments)" and "0 total" are evidence of no claim, not missing evidence.

Why this form:
- A good-first-issue label is not a claim that the issue is free, so the check reads all three
  places a claim lives: the assignee, linked PRs (including fork PRs such as issue-03's
  `quick123-666/pylint#1 (open)`), and the thread.
- The 90-day window and the "stale" sentence exist for issue-09. Its 2022 claim ("I'd like to
  take a swing at this") was answered by the maintainer with "Think you can just give it a
  try", and gold accepts it.
- The R6 sentence was added after run 2. issue-15 shows "Comments (97 total, first 40 shown)",
  so the 57 hidden comments are the newest ones. The check had passed it on "last shown claim
  (souvik150, 2024-02-16)", which is silence it could not actually see.

**Trade-offs**

- **What it changes:** with the R6 sentence, issue-15's `not-claimed` went from `pass` to
  `unclear`: "57 newest comments hidden per R6, could contain a claim within 90 days of
  capture". The verdict stayed `reject`, but it no longer rests on `bounded-scope` alone.
- **Canaries re-run with `--only` (run 4, 5/5):**
  - issue-09 (a stale claim that must still pass) stayed `accept`.
  - issue-08, issue-18 and issue-12 stayed `reject` for their original reasons.
- **Why nothing changed elsewhere:** only four bundles have truncated threads (calib-04 22/23,
  issue-05 40/106, issue-10 4/5, issue-15 40/97), and all four are gold `reject`. No
  gold-`accept` item can be touched by R6. Full run 5 confirmed it at 20/20.
- **What it gives up:** a genuinely free issue with a long thread would be rejected in eval mode
  as `unclear`. I accept that miss, because live mode reads the whole thread.
- **Live-mode cost:** Path Review's house rule tells the skill to ignore classmates' claim
  comments, so condition (c) is switched off there. In the live run, #69 had three classmate
  claims and still passed. The skill itself flagged that my `bounded-scope` clause (f) ("three or
  more different people have claimed it") reads literally against #69. It suggested requiring at
  least one opened PR before (f) can fire. I have not made that change yet.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit and time.** #72 is a fail-open authentication bug: `verify_password` raises
   `UnknownHashError` on a malformed stored hash instead of returning False. I've used Python
   throughout my career. Making a security check fail closed is the guardrail and trustworthy-AI
   ground I work on at the UCLA Trustworthy AI Lab. It's also a clean test-first exercise: write
   the failing test for a malformed hash, then make it pass. The skill judged it a single-file
   fix, which fits the time I have alongside research and contract work.
2. **What the verdict got right, and what it couldn't weigh.**
   - Right: the repo is alive, there's no assignee or open PR, the scope is bounded (a
     maintainer-filed bug that names its cause), and CONTRIBUTING.md is silent on AI.
   - Couldn't weigh: whether the fix changes behaviour other code relies on (callers might
     expect an exception). It also couldn't weigh whether a malformed hash should be logged as a
     possible tampering signal rather than silently treated as a wrong password. I'll check both
     before planning in Unit 3.
3. **Claiming difficulty.** One classmate has already posted a claim comment on #72. Under the
   Path Review house rule that doesn't block me, but my claim needs to show a distinct plan.
   `maintainer-responsive` failed: none of the five sampled issues had a staff reply. So my claim
   may go unacknowledged for a while, and I should plan to start from the reproduction rather
   than wait for a reply. I'll write the claim in Unit 2 with the voice guide.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
