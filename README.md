# Reusable

## Reusable Renovate config

[`./renovate-config/default.jsonc`](./renovate-config/default.jsonc)

## Reusable GitHub Actions

### `ppmcheckpdf-deps`

Install dependencies for [`ppmcheckpdf`](https://ctan.org/pkg/ppmcheckpdf)
LaTeX package or the [`ppmcheckpdf.lua`][ppmcheckpdf.lua] in
`muzimuzhi/latex-zutil` repository.

[ppmcheckpdf.lua]: https://github.com/muzimuzhi/latex-zutil/blob/main/support/ppmcheckpdf.lua

### `setup-pre-commit-uv` (deprecated on 2026-09-15)

[`muzimuzhi/latex-util@5dcc828`][muzimuzhi/latex-util@5dcc828] (ci(lint): install `pre-commit` using `mise`, 2026-09-15) replaced its only use with `mise`.

[muzimuzhi/latex-util@5dcc828]: https://github.com/muzimuzhi/latex-zutil/commit/5dcc8288a4cecb8e2be3cc3329a24c1bd852d8ce

<details>
<summary>old doc</summary>

Install [`pre-commit`][pre-commit] using [`uv`][uv], init it and setup caching

All inputs are optional.

```yaml
# default values of all inputs
- name: Setup pre-commit
  uses: muzimuzhi/reusable/actions/setup-pre-commit-uv@main
  with:
    setup-uv: true
    version: 'latest'
    config: '.pre-commit-config.yaml'
    run-pre-commit: true
    args: '--all-files --show-diff-on-failure --color=always'
```

`uv` cache is disabled by default ([why][why-disable-uv-cache]). If needed,
setup `uv` beforehand, then use this action with `setup-uv: false`.

```yaml
- name: Setup uv
  # since v8.0.0, astral-sh/setup-uv stopped providing major and minor tags
  uses: astral-sh/setup-uv@v8.2.0
  with:
    enable-cache: true # enabled on GitHub-hosted runners by default

- name: Setup pre-commit
  uses: muzimuzhi/reusable/actions/setup-pre-commit-uv@main
  with:
    setup-uv: false
```

[pre-commit]: https://github.com/pre-commit/pre-commit
[uv]: https://github.com/astral-sh/uv
[why-disable-uv-cache]: https://github.com/astral-sh/setup-uv/tree/v6/?tab=readme-ov-file#disable-cache-pruning

</details>

### `unique-id`

Generate a `unique_id` output (in snake case) for use in e.g., archives. Also exported to environment variable by default.
