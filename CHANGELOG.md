# Changelog

## [Unreleased]
- Naming convention: git now tracks the lowercase directory names `assets/ css/ inc/ js/ sub/` (the working tree already had them, but the git index still held `Assets/ Css/ Inc/ Js/ Sub/` because macOS's case-insensitive filesystem hid the rename). **Breaking for case-sensitive checkouts (Linux/Plesk) of earlier versions:** they contained the capitalised names, so `inc/footer.php`, `sub/404.php` etc. did not resolve there; after this version they do. Sites cloned from this template that still use the capitalised directories on Linux must rename them (`git mv Inc inc_tmp && git mv inc_tmp inc`, etc.). Also stopped tracking `Sub/.DS_Store`.
- Added `deploy/post-deploy.sh`, following the same pattern used to fix a confirmed ecosystem-wide
  deploy bug in every `rio-*-server` repo: Plesk's git "pull" deploy mode file-copies a repo into
  each vhost with no `.git` present, so every `submodules/<name>/` directory arrives completely
  empty (a git submodule is a commit reference, not files). The script re-clones/updates each of
  the 4 submodules (`rio-website`, `rio-style`, `rio-monitor-sdk`, `rio-translation-sdk`) as its
  own independent git checkout, tracking each one's `production` branch tip. **Not currently
  usable**: as of 2026-08-26 neither a `development` nor `production` vhost exists for this repo
  in Plesk (no deploymentPath entry, no vhost directory on disk) — this repo is a scaffold that
  other plain-PHP Rio websites are cloned from, not itself deployed today. Written ahead of any
  future vhost for consistency with the rest of the ecosystem's fix; see CLAUDE.md's "What this
  is" section for the reconciled description.
- Initial scaffold: folder layout, vendored front-end plugins, `.htaccess` with cache headers and
  versioned-asset rewriting, and git submodule wiring for shared Rio site dependencies.
- Standardized submodule paths to `submodules/rio-x` and updated to renamed dependencies.
- Added README per ecosystem guideline.
