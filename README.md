# site-generator-speed-01-run-20261122

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/kuyang300/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/kuyang300/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's own makefun-site 1.0.0: `solve.js` answers every
case exactly as makefun-site does — same front matter, template dialect,
Markdown subset, slug rule and build report, byte for byte — with less work.
`main.ts` is the driver the harness runs: it reads every case from
`/input/cases.json`, answers each with `run`, and writes `/output/answers.json`.

Where the speed comes from:

- Markdown is lexed and rendered in one pass, so no token objects are built.
- Inline text is escaped in bulk runs instead of one regex call per character.
- Slugs skip Unicode normalisation on pure-ASCII text (NFKD has no
  decomposition for an ASCII character and no ASCII character is a mark).
- Template output is built in a parts array instead of string concatenation,
  and the render scope chains the shared `site` / `tags` / `recent` values
  instead of copying them per page.
- Each page's card is built once and reused by every list and page that shows
  it; each tag's slug is computed once per name, not once per use.

## Run it

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=<cases dir> MAKEFUN_OUTPUT_DIR=out node main.ts
```

Node 22, no dependencies, no network, no files read at run time: `run(input)`
is a function of its input alone. It runs twice with identical output.

---

<sub>Entered on [make.fun](https://make.fun/?ref=ev664qf8&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
