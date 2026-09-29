<p align="center">
  <img src="https://cdn.prod.website-files.com/69a0c4f8849f7ba068f89485/69a0c4f8849f7ba068f894ba_Background%20Colour%3DDark%20Background.svg" alt="YLD" width="200">
</p>

# YLD Skills

Shared skills for AI coding agents, maintained for everyone at YLD.

## What this is

A skill is a folder with a `SKILL.md` file in it. The file tells an agent how to do one kind of task well, such as running a release or writing a status update in the way we expect. When the agent sees a matching request it loads the instructions and follows them. A skill can also carry scripts, templates and reference documents that the agent reads only when it needs them.

This repository holds the skills specific to how YLD works, the ones we want every YLD engineer to have. Keeping them in one place means a fix lands once and everyone picks it up on their next pull, instead of each person maintaining their own copy.

The folders follow the open [Agent Skills](https://agentskills.io) format, so they work in Claude Code and in any other tool that supports it.

## Using the skills

The easiest way is the [skills.sh](https://skills.sh) CLI, which you run with npx so there is nothing to install first. It detects the agents you have and puts each skill where that agent reads from:

```sh
npx skills add yldio/skills
```

That lists the skills in this repository and asks which ones you want and which agents to install them for. Useful variants:

```sh
# All skills, personal install (user-level, e.g. ~/.claude/skills)
npx skills add yldio/skills -s '*' -g

# Just one skill
npx skills add yldio/skills -s forensic-report

# For specific agents (repeat -a for more than one)
npx skills add yldio/skills -a claude-code
```

Without `-g` the skill installs into the current project, which is what you want when it should apply only within one project. With `-g` it installs once for your account and is available in every project.

Managing installed skills:

```sh
npx skills update          # bring installed skills up to date
npx skills list            # which skills are installed and where
npx skills remove <name>   # uninstall a skill
```

Start a new session and the skills are available. In Claude Code you can call one directly with `/<skill-name>`, or describe the task and let the agent choose.

### Without the skills CLI

If you would rather skip npx, clone the repository somewhere you will keep it:

```sh
git clone git@github.com:yldio/skills.git ~/yld/skills
```

Link the skills you want into the directory your tool reads from. Claude Code reads personal skills from `~/.claude/skills`:

```sh
mkdir -p ~/.claude/skills
ln -s ~/yld/skills/<skill-name> ~/.claude/skills/<skill-name>
```

To make all of them available at once:

```sh
mkdir -p ~/.claude/skills
for d in ~/yld/skills/*/; do
  ln -sfn "$d" ~/.claude/skills/$(basename "$d")
done
```

Run `git pull` in your clone now and then to get updates. Skills installed this way are not tracked by `npx skills list` or `npx skills update`.

## Community skills

Standard skills for widely used tools and frameworks already exist in public collections, for example [anthropics/skills](https://github.com/anthropics/skills). Use those rather than writing our own version. Install them the same way as the skills in this repository, for example `npx skills add anthropics/skills`, or clone the collection and link the folders you want into `~/.claude/skills`.

If you find a community skill worth recommending to everyone at YLD, open a pull request that adds a link to it in this section. Do not copy the files into this repository, as the copy will drift from the original and nobody will maintain it.

## Adding or changing a skill

1. Create a folder named after the skill, lowercase with hyphens. This name is what people will type.
2. Write `SKILL.md` with frontmatter followed by the instructions:

   ```markdown
   ---
   name: release-notes
   description: Draft release notes from merged pull requests. Use when asked to write or publish release notes for a version.
   ---

   The instructions the agent follows once the skill is loaded.
   ```

   The description decides when the agent picks the skill, so state what it does and when it applies. Keep the body short and specific. Long reference material goes in separate files in the same folder, with a line in `SKILL.md` telling the agent when to read them.
3. If the skill should run only when a person asks for it, add `disable-model-invocation: true` to the frontmatter:

   ```markdown
   ---
   name: deploy-production
   description: Deploy the current release to production.
   disable-model-invocation: true
   ---
   ```

   The agent will then never start the skill on its own. The only way to run it is to type `/deploy-production`. Use this for anything with side effects, such as deploying, publishing or sending messages, where the agent guessing wrong would cost something.
4. Put helper scripts in `scripts/`, templates in `assets/` and background reading in `references/`.
5. Try it on a real task before opening a pull request. Put the prompt you used and what came out in the PR description.
6. Open a pull request against `main`.

Write skills for the whole company rather than for one project. A skill that only makes sense inside one codebase belongs in that codebase.

## Rules

- No model pinning. Do not set `model` in a skill's frontmatter. Skills run on whatever model the person using them has chosen, and a pinned model stops working when that model is retired.
- No credentials, tokens or keys anywhere in this repository, including in examples and test fixtures.
- No client names, client code or client data. If a skill grew out of client work, strip anything that identifies the client before contributing it.
- If a skill sends anything to an external service, say so plainly in its `SKILL.md` so the person running it knows beforehand.

## Licence

Apache 2.0. See [LICENSE](LICENSE).
