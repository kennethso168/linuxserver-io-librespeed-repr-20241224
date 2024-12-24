# minimal-reproduction-template

<!--First, read the [Renovate minimal reproduction instructions](https://github.com/renovatebot/renovate/blob/main/docs/development/minimal-reproductions.md).

Then replace the current `h1` with the Renovate Issue/Discussion number.-->

This repo reproduces that for linuxserver.io docker images in docker compose files using regular expression versioning, update PRs are only raised when the regex defines the capture groups `major`, `minor`, `patch` and `build`, and not raised with the capture groups `major`, `minor`, `patch` and `revision` [as per the example in docs](https://docs.renovatebot.com/modules/versioning/regex/#description).

## Current behavior

At commit [cb0a777](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/tree/cb0a77756580e84543d7fe8e9962a4572eaa065c) the key values are as below:

[compose.yml](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/blob/cb0a77756580e84543d7fe8e9962a4572eaa065c/compose.yml):

`image: ghcr.io/linuxserver/librespeed:5.4.1-ls215`

[renovate.json](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/blob/cb0a77756580e84543d7fe8e9962a4572eaa065c/renovate.json):

`"versioning": "regex:^(?<major>\\d+)\\.(?<minor>\\d+)\\.(?<patch>\\d+)-ls(?<revision>.+)$"`

No PRs were opened by renovate for updates. [Job run log](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/blob/main/job_log/log1)

Afterwards, at commit [8dcdb68](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/commit/8dcdb6820b323f12a72a8560296b9c434f183c22), which changes the `revision` capture group to `build`, [PR #3](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/pull/3) for updating to version `5.4.1-ls218` was successfully opened by renovate. [Job run log](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/blob/main/job_log/log2)

Thereafter, at commit [9ef6d26](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/commit/9ef6d268237dbb107889f95024904e7b700ff04e), which reverted the previous commit, renovate auto closed the PR. [Job run log](https://github.com/kennethso168/linuxserver-io-librespeed-repr-20241224/blob/main/job_log/log3)

## Expected behavior

I expected that examples should work, so at commit cb0a777 renovate should be able to open a PR suggesting a patch update to the version `5.4.1-ls218`.

If this is not the intended behavior, the docs should be updated.

## Link to the Renovate issue or Discussion

Put your link to the Renovate issue or Discussion here.
