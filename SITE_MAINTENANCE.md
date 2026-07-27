# Site maintenance

This repository publishes Huan Xu's academic website at <https://xuhuanhydro.github.io>. Keep public claims evidence-based; do not add private data, credentials, unpublished results, or unverified publication metadata.

## Content map

1. **Home:** edit `_pages/about.md`.
2. **Research:** edit `_pages/research.md`; distinguish research questions from completed findings.
3. **Publications:** add one verified Markdown record per paper under `_publications/`, following Academic Pages front matter. Verify title, full author list, venue, year, and DOI or journal URL before publication.
4. **Software:** edit `_pages/software.md`. List only public, non-fork research repositories with an accurate release status.
5. **Writing:** copy `_drafts/writing-template.md` to `_posts/YYYY-MM-DD-short-title.md`, replace all placeholders, remove `published: false`, and build locally before release.
6. **CV:** replace `_pages/cv.md` with verified content. To offer a PDF, save it as `files/Huan_Xu_CV.pdf` and add a link to `/files/Huan_Xu_CV.pdf`.
7. **Portrait:** save a confirmed image under `images/`, then set `author.avatar` in `_config.yml` to its filename. Do not use an inferred or third-party photo.

## Local preview

With Ruby and Bundler installed:

```powershell
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll build
bundle exec jekyll serve -l -H localhost
```

Open <http://localhost:4000>. Configuration changes require restarting Jekyll. Docker users may instead run `docker compose up`.

## Deployment checks

Push `main`, then open the repository's **Actions** tab and wait for the GitHub Pages build and deployment to succeed. In **Settings → Pages**, the source must be the `main` branch at `/ (root)`, matching this repository's Jekyll layout.

If deployment fails:

1. Open the failed run and identify the first build error.
2. Reproduce it with `bundle exec jekyll build`.
3. Correct only the relevant YAML, Liquid, dependency, or path error.
4. Rebuild locally, commit, push, and verify all six navigation routes.

Do not force-push deployment fixes or replace the official build flow without evidence that the current flow is incompatible.

## Current placeholders

- Confirmed portrait
- Complete CV and optional PDF
- Verified publication metadata
- Public email, Google Scholar, ORCID, and LinkedIn
- Future writing posts
