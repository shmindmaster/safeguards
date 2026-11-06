# safeguards

Dataset of written-safeguard coverage for 356 public AI system prompts, plus
the script that regenerates it. The checkout is
`C:\Repos\shmindmaster\safeguards`. There is no `apps/` tree and no server.

`scoring/` owns the rules and the generator. `data/` and `figures/` are the
committed outputs. `docs/RESULTS.md` is generated. `docs/` has ten evergreen
documents plus this pattern's local `AGENTS.md` files. `hf/README.md` is the
Hugging Face card. `infra/docker/` is the only image.

## Commands

```text
docker compose run --build --rm test
docker compose run --build --rm score
```

`test` is offline. `score` fetches the pinned upstream commits into the
`safeguards-cache` volume and fails if a generated file drifted. Do not create
a virtual environment or a `.cache` directory in the checkout.

## Rules

- Do not add prompt text, quotations, or a `.cache` checkout to the repo.
- Do not hand-edit `data/*.csv`, `data/summary.json`, `docs/RESULTS.md`, or
  `figures/controls-by-source.svg`. Change the generator and re-run `score`.
- A ruleset or source change bumps the version in `data/summary.json`.
- Code is Apache-2.0. Data is CC BY 4.0. `NOTICE` records the split.
- The nearest `AGENTS.md` adds local rules. The root file still applies.

## Done

Both compose commands pass. Docs match the code. Commit. There is no
production host. `main` plus a green `score` run is the release.
