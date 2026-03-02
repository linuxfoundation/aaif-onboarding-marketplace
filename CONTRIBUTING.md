# Contributing to AAIF Onboarding Marketplace

Thank you for your interest in contributing to the AAIF Onboarding Marketplace plugin.

## Developer Certificate of Origin (DCO)

All contributions to this project **must** be signed off under the
[Developer Certificate of Origin](https://developercertificate.org/) (DCO).
This is a lightweight agreement that certifies you wrote (or have the right to
submit) the contribution.

### How to sign off

Add a `Signed-off-by` trailer to every commit:

```bash
git commit -s -m "Your commit message"
```

This appends a line like:

```
Signed-off-by: Your Name <your.email@example.com>
```

If you forget, amend the most recent commit:

```bash
git commit --amend -s
```

> **CI enforcement**: A DCO check runs on every pull request. Unsigned commits
> will block the PR from merging.

## Getting Started

1. Fork this repository
2. Clone your fork:
   ```bash
   git clone git@github.com:linuxfoundation/aaif-onboarding-marketplace.git
   cd aaif-onboarding-marketplace
   ```
3. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature
   ```

## Repository Structure

```
aaif-onboarding-marketplace/
├── .claude-plugin/         # Plugin metadata
├── plugins/
│   └── aaif-onboarding/    # Plugin skills and commands
├── aaif-onboarding-cowork.plugin  # Plugin definition
└── README.md
```

## What to Contribute

- New skills or commands for the onboarding plugin
- Bug fixes in plugin configuration
- Documentation improvements
- Testing and validation of plugin behavior

## Pull Request Process

1. Ensure your changes work with the AAIF MCP Server backend
2. Update the README if you add new capabilities
3. All commits must be signed off (DCO)
4. Request a review from `@manishdixitlfx`

## Code of Conduct

This project follows the
[Linux Foundation Code of Conduct](https://lfprojects.org/policies/code-of-conduct/).

## License

By contributing, you agree that your contributions will be licensed under the
[Apache License 2.0](./LICENSE).
