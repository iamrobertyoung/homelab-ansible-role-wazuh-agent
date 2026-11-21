# Contributing

Thank you for considering contributing to this Ansible role.

## Development Setup

1. **Prerequisites**
   - Python 3.13+
   - Docker (for Molecule testing)
   - [mise](https://mise.jdx.dev/) for tool version management

2. **Install dependencies**
   ```bash
   mise install
   pip install -r requirements.txt
   pre-commit install
   ```

## Testing

This role uses [Molecule](https://molecule.readthedocs.io/) for testing with Docker.

```bash
molecule test          # Run full test suite
molecule converge      # Apply role to test container
molecule verify        # Run verification only
molecule login         # Access container for debugging
molecule destroy       # Clean up test containers
```

## Linting

```bash
yamllint .             # Lint all YAML files
ansible-lint           # Lint Ansible code
pre-commit run --all-files  # Run all pre-commit hooks
```

## Commit Convention

This project uses [Conventional Commits](https://www.conventionalcommits.org/) with semantic-release for automated versioning.

**Commit prefixes:**
- `feat:` - New feature (minor version bump)
- `fix:` - Bug fix (patch version bump)
- `docs:` - Documentation changes
- `refactor:` - Code refactoring
- `perf:` - Performance improvements
- `test:` - Adding or updating tests
- `ci:` - CI/CD changes
- `chore:` - Maintenance tasks

**Examples:**
```
feat: add support for custom log paths
fix: correct file permissions on ossec.conf
docs: update variable documentation in README
```

## Pull Request Process

1. Fork the repository and create a feature branch
2. Make your changes following the coding standards
3. Ensure all tests pass (`molecule test`)
4. Ensure linting passes (`yamllint .` and `ansible-lint`)
5. Commit using conventional commit format
6. Open a pull request with a clear description

## YAML Style

- Maximum line length: 120 characters
- Truthy values: use `true`/`false` or `yes`/`no`
- Minimum 1 space after comment markers

## Questions?

Open an issue for questions or discussion.
