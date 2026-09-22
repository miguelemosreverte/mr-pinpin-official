# Publishing rules

Read `README.md` first. This is `miguelemosreverte/mr-pinpin-official`.
Authoring belongs in `https://github.com/miguelemosreverte/mr-pinpin-source`;
follow that repository's `PUBLISHING.md` and `tools/publishing/README.md`.

This is a deployment-only repo. Do not add authoring history or site binaries.
Never edit/delete releases/<sha>.json or rewrite published HF objects. New
releases add new records; rollback only changes release.json to an existing SHA.
Use the authoring repo's tools/publishing CLI, normal commits, and normal pushes.
Do not bypass archive/file verification or raise the 950,000,000-byte size cap.
HF public downloads require no credentials. Do not add secrets to this repo.
No deployment or old-site cutover without the operator's authorization.
