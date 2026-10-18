# pr

Writes a PR body. It uses the repo's own PR template from `.github` when there is one, and falls back to a default Summary / Evidence / Merge Danger template when there isn't.

## Credits

This skill is adapted from the [`pr` skill](https://github.com/mattpocock/skills/blob/main/skills/engineering/pr/SKILL.md) by [Matt Pocock](https://github.com/mattpocock), which builds on the [`show-me` skill](https://github.com/humanlayer/skills/blob/main/plugins/show-me/skills/show-me/SKILL.md) by Dex Horthy at [HumanLayer](https://github.com/humanlayer). The default template and the guidance on writing each section are theirs.

The change here: the skill prefers the caller repo's own PR template, and only uses Matt's template when the repo has none.
