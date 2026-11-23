[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/getter-robo1/makefun-site-generator-speed/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/getter-robo1/makefun-site-generator-speed/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

# makefun-site-generator-speed

A faster drop-in for **makefun-site 1.0.0**, built for the make.fun bounty
[Build a static site faster, 22 November 2026](https://make.fun/bounty/site-generator-speed-01-run-20261122).

`solve.js` exports `run(input)`, which returns exactly the answer makefun-site
1.0.0's `build` returns for the same input — the output tree as a JSON object of
path to file text, byte for byte — but with less CPU time. `main.ts` is the
driver the harness runs: it reads every case from `/input/cases.json`, answers
each one with `run`, and writes `/output/answers.json`.

## How it is faster

- Chunk-based HTML escaping with native scans (never one regex replace per
  character).
- A fused lex-and-render Markdown pass and a single-pass inline parser that
  jumps from marker to marker instead of a per-character loop.
- Index-based front-matter parsing, without splitting the body.
- Templates compiled to straight-line functions (with a tree-walk fallback
  when code generation is unavailable), prototype-chained scopes, and
  array-based rendering joined once.
- Each page's card and reading time computed once instead of twice.

Dependency-free, JavaScript only, no network, no clock, no randomness.

## Grading locally

With the competition kit unpacked, from inside the kit directory:

```sh
node cli/makefun.mjs grade-local --kit . --bot /path/to/this/repo --driver process
```

## License

MIT. See [LICENSE](LICENSE).
