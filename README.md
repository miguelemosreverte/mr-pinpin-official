# Mr. PinPin Pages

Public site: https://miguelemosreverte.github.io/mr-pinpin-pages/
Authoring repository: https://github.com/miguelemosreverte/mr-pinpin-original
Public release bucket: https://huggingface.co/buckets/miguelemosreverte/mr-pinpin-archive

Deployment-only repository: miguelemosreverte/mr-pinpin-pages. Source, asset
authoring, and build history remain in the authoring repository. No site binaries
or source history belong in this repo.

release.json selects a SHA-256-addressed releases/<sha>.json. The manifest records
the source commit, exact archive identity, and every site file's bytes and SHA-256.
CI downloads anonymously from the public Hugging Face bucket and verifies all of
them before deploying. No HF secret is needed. Set Pages source to GitHub Actions.

Run locally: python3 scripts/materialize.py --repo . --out NEW_OUTPUT_DIRECTORY
The Python materializer uses only the standard library and never replaces an
existing output. URLs and paths inside the built site are preserved unchanged.

To publish or roll back, use tools/publishing/publish.py in the authoring repo:
stage --package PACKAGE --pages-repo THIS_REPO adds an immutable release record;
select --pages-repo THIS_REPO --release SHA --expected-current OLD_SHA explicitly
updates the selector. Review, commit, and push normally. Never force-push. Keep
older release records and HF objects so rollback remains available. First-time
template generation includes the initial selected manifest.

HF buckets are mutable storage, not provider WORM. Hash keys, refusal to overwrite
conflicting content, verified upload readback, and anonymous deployment checks
enforce immutability at the application level. Never replace/delete release
objects. External mutation causes verification failure, not silent deployment.
The script does not create repositories, configure Pages, commit, push, or cut
over traffic. The old site stays live until its operator explicitly changes it.
