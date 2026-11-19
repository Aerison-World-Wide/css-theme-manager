# css-theme-manager — fork design (Paul's spec, 2026-11-19)

Intent (Paul): fix the project, then fork it. Make it do what
templates do. On-the-fly modular. Nothing hard coded — everything
pulls from lists and arrays stored on the target.

## Addressing (Paul's notation)

{template_path=<https://sub.domain.tld/templates/<templateid>.tmp;}

A template is a FILE addressed by pattern: a base path holding
per-template files named <templateid>.tmp. The engine holds no
template content; it holds the path pattern and substitutes the
id. Templates live on the target (the site's own host), not in
the library and not in the consuming page.

## Model

- A MANIFEST at the target lists what exists (a list/array:
  ids, names, kinds, which is default). The engine fetches the
  manifest; the manifest is the only thing it needs to know.
- A .tmp file is structured data (JSON shape): lists and arrays
  all the way down — token sets (CSS variables), element blocks,
  layout fragments. Nothing in the engine assumes a key exists;
  it applies what the file declares.
- Kinds: theme (token set) first — the original project's job —
  with the format open to further template kinds later.
- Apply is scoped (the original's one good idea, kept): a
  template applies to :root or to any selector.
- Persistence is PLUGGABLE: the engine emits change events and
  accepts an initial selection; it does not reach for
  localStorage itself. (In Tax Tally, the storage adapter is the
  funnel; in BTSS, its template system will be.)
- No forced variable prefix (the original's csstm- was a
  hard-code; a prefix is a manifest/setting choice or absent).

## API sketch (lineage from the original, generalized)

- createEngine({ templatePath, manifestUrl, store? })
- engine.list()            -> the manifest array
- engine.load(id)          -> fetch + register a .tmp, on the fly
- engine.apply(id, selector = ':root')
- engine.remove(id)
- engine.onChange(fn)      -> persistence hooks live outside

## The pipeline (Paul's goal, translated 2026-11-19 13:33 CT)

1. A published version exists outside the org (upstream,
   WendellAdriel/css-theme-manager, public).
2. A fork brings that version INTO the org.
3. Edits and commits land in the org fork — modification and
   optimization, with history.
4. At maturity: collapse the commit series to a clean public
   state and merge the branch back into the ORIGINAL as a
   contribution (a pull request upstream).

Consequence: step 4 requires the REGISTERED fork (fork-network
membership) — a mirror copy cannot open a PR to upstream. That
settles the terminology question for this project: "fork" here
means the GitHub-registered sense, and the fork step itself is
the one operation still blocked (App-token 403; route is Paul's
UI fork into the org, or a one-card API test to his personal
account as a diagnostic).

## Licensing

Upstream is MIT (Wendell Adriel) — the fork keeps the MIT notice
for the original code. Paul's additions: license to be ruled
(house noncommercial copyleft vs keeping the fork MIT for the
commons — Paul's call; "join the fabric to the web" argues MIT).

## Status

FORKED (Paul, via the GitHub UI, 2026-11-19 ~13:45 CT):
Aerison-World-Wide/css-theme-manager is a registered fork of
WendellAdriel/css-theme-manager. Verified at landing: 4 commits,
HEAD 550b0659986915c6cde21248128f28b515614bf9 -- bit-identical
to upstream, tag v1.0.0 in history, no time travel. The App
could not fork or create in the org (role-scoped installation:
push to selected repos only); Paul's click supplied the one
step behind that wall, and the ideal pipeline (fork -> edit ->
commit -> merge back as a contribution) is intact. Working
mode for now: our silo -- a divergent line with attribution --
with the merge-back held for maturity. This document lands as
the rebuild's opening commit.
