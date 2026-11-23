# Zed release controls

Release publication is manual. Merge the reviewed release commit to `master`, create the matching `vMAJOR.MINOR.PATCH` tag on that commit and publish the GitHub Release. While that commit is still the selected `master` tip, dispatch **Release Zed Extension** with the explicit tag. The workflow verifies the tag and version before requesting production approval. It intentionally does not release an older or differently tagged commit.

## Repository-owner setup before merging

- Protect `master`: require reviewed pull requests, restrict direct pushes and force pushes, and require code-owner review of publishing workflow changes. Limit any bypass and review release-related repository roles.
- Restrict creation, modification and deletion of `v*` tags to authorized release managers; keep release tags immutable after creation.
- Create the `zed-registry-production` environment. Allow only the `master` branch, no tags, require a designated independent reviewer and disable self-review and administrator bypass wherever available.
- Provision `ZED_REGISTRY_RELEASE_TOKEN` **only** as an environment secret, using the least access required for the registry fork update and upstream PR. Validate the necessary scope separately; do not grant broad rights to unrelated repositories. Remove the old repository/organisation credential grant and revoke its token before relying on the new boundary. Do not add any replacement at repository or organisation scope.

A workflow file does not configure the repository or environment policies. Verify them before enabling publication. If a gate is unavailable, stop rather than dispatching from another ref or using an unreviewed token.
