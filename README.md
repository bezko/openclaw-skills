# OpenClaw Skills

A collection of skills for OpenClaw.

## Skills

### astro

Deploy multilingual static websites for free on Cloudflare using Astro framework with markdown source files.

```bash
# Install skill
clawhub install astro
```

### glab

GitLab CLI for managing issues, merge requests, CI/CD pipelines, and repositories.

```bash
# Install skill
clawhub install glab

# Requires: glab, jq, GITLAB_TOKEN
```

## Installing Skills

```bash
# Install specific skill
clawhub install astro
clawhub install glab

# Or install from repo
clawhub install bezko/openclaw-skills/skills/astro
```

## Publishing Skills

Skills in this repository follow ClawHub standards and can be published to [clawhub.com](https://clawhub.com).

```bash
# Publish to ClawHub
clawhub publish ./skills/glab --slug glab --name "glab" --version 1.0.2
```

## Contributing

1. Fork this repository
2. Create a new skill in `skills/<skill-name>/`
3. Include `SKILL.md` with proper frontmatter
4. Add scripts in `scripts/` (Python/Bash, minimal dependencies)
5. Submit a pull request

## License

MIT
