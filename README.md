# Mr. PinPin Official

The official published books and interactive atlas. This repository deploys
verified releases; it is not where stories, illustrations, or application code
are edited.

**Read:** [Books](https://miguelemosreverte.github.io/mr-pinpin-official/storyboard/library.html)
| [Atlas](https://miguelemosreverte.github.io/mr-pinpin-official/storyboard/atlas-webgpu.html)
| [Original book](https://miguelemosreverte.github.io/mr-pinpin-official/)

## Where to work

| Location | Responsibility |
| --- | --- |
| [mr-pinpin-source](https://github.com/miguelemosreverte/mr-pinpin-source) | Edit stories, translations, application code, and artwork provenance. Build and test releases. |
| This repository | Select and deploy a verified release. Keep it small: no artwork, video, or archive blobs in Git. |
| [Public Hugging Face storage](https://huggingface.co/buckets/miguelemosreverte/mr-pinpin-archive) | Preserve originals, production assets, and content-addressed release bundles. |

Start with the source repository's [publishing guide](https://github.com/miguelemosreverte/mr-pinpin-source/blob/main/PUBLISHING.md).

## Files you need

| File | Purpose |
| --- | --- |
| `release.json` | Selects the release that the next deployment will publish. |
| `releases/<sha>.json` | Immutable release record: source commit, archive identity, and every site file's checksum. Never edit or delete an existing record. |
| `scripts/materialize.py` | Downloads and verifies the selected release into a new directory. |
| `.github/workflows/pages.yml` | Verifies and deploys on a push to `main`, or an explicit workflow run. |
| `AGENTS.md` | Safety rules for agents working here. |

## Restore locally

Requires Python 3.10 or newer; no external Python packages or HF token:

```sh
python3 scripts/materialize.py --repo . --out NEW_OUTPUT_DIRECTORY
```

Use a new output directory on a disk with space for the download and extracted
site. The command refuses to replace existing output and checks every file.

## Publish or roll back

Build, package, upload, and verify from `mr-pinpin-source` using its
[release CLI](https://github.com/miguelemosreverte/mr-pinpin-source/tree/main/tools/publishing).
Then, from that source checkout:

```sh
npm run release -- stage --package PACKAGE_DIRECTORY --pages-repo OFFICIAL_CHECKOUT
npm run release -- select --pages-repo OFFICIAL_CHECKOUT \
  --release NEW_RELEASE_SHA --expected-current CURRENT_RELEASE_SHA
```

Review the change, commit, and push normally in this repository. Wait for the
deployment to succeed and check the public book and atlas. Rollback uses the same
`select` command with a previous release SHA, followed by a new commit. Never
force-push. Keep previous records and HF objects.

CI downloads anonymously, verifies the archive and all files, and only then
deploys. Readers receive assets from Pages, not HF. Bucket storage is mutable,
not provider-enforced write-once retention; checksums detect altered bytes.

## Previous names

This repository was `mr-pinpin-pages`; the source was `mr-pinpin-original`.
GitHub repository links redirect, but old Pages URLs do not automatically
redirect. Use the official reader links above. Historical release records and
their source commit IDs remain unchanged and valid.
