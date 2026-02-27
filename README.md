# OpenClaw Skills

A collection of skills for OpenClaw.

## Skills

### astro

Deploy multilingual static websites for free on Cloudflare using Astro framework with markdown source files.

```bash
# Install skill
clawhub install astro

# Use in OpenClaw
# The skill triggers automatically when creating static sites, 
# setting up multilingual content, or deploying to Cloudflare Pages.
```

## Installing Skills

```bash
# Install all skills from this repo
clawhub install bezko/openclaw-skills

# Install specific skill
clawhub install bezko/openclaw-skills/skills/astro
```

## Publishing Skills

Skills in this repository follow ClawHub standards and can be published to [clawhub.com](https://clawhub.com).

```bash
# Package a skill
cd skills/astro
clawhub package .

# Publish to ClawHub
clawhub publish astro.skill
```

## Contributing

1. Fork this repository
2. Create a new skill in `skills/<skill-name>/`
3. Include `SKILL.md` with proper frontmatter
4. Add scripts in `scripts/` (Python, no dependencies)
5. Submit a pull request

## License

MIT
