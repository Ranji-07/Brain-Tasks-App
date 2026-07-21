# Contributing to Brain-Tasks-App

First off, thank you for considering contributing to **Brain-Tasks-App**! It's people like you that make this infrastructure project such a great resource.

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the issue list as you might find out that you don't need to create one. When you are creating a bug report, please include as many details as possible:

- **Use a clear and descriptive title**
- **Describe the exact steps which reproduce the problem**
- **Provide specific examples to demonstrate the steps**
- **Describe the behavior you observed after following the steps**
- **Explain which behavior you expected to see instead and why**
- **Include Terraform configuration** (sanitized for secrets)
- **Include environment details** (OS, Terraform version, AWS region)

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, please include:

- **Use a clear and descriptive title**
- **Provide a step-by-step description of the suggested enhancement**
- **Provide specific examples to demonstrate the steps**
- **Describe the current behavior and the expected behavior**
- **Explain why this enhancement would be useful**

### Pull Requests

- Follow the [HCL Style Guide](https://developer.hashicorp.com/terraform/language/syntax/style)
- Use descriptive variable names
- Add comments for complex logic
- Update documentation
- Write meaningful commit messages
- Include test configurations

#### Pull Request Process

1. Fork the repository and create your branch from `main`
2. Update README.md with details of changes if applicable
3. Add comments to complex Terraform configurations
4. Ensure configuration validates: `terraform validate`
5. Format code: `terraform fmt -recursive`
6. Submit a Pull Request with a clear description

## Development Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/Ranji-07/Brain-Tasks-App.git
   cd Brain-Tasks-App
   ```

2. **Create a new branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Install Terraform**
   ```bash
   brew install terraform  # macOS
   ```

4. **Make your changes**

5. **Validate and format**
   ```bash
   terraform validate
   terraform fmt -recursive
   ```

6. **Commit and push**
   ```bash
   git add .
   git commit -m "feat: describe your feature"
   git push origin feature/your-feature-name
   ```

## Styleguides

### HCL Code Style

- Use consistent indentation (2 spaces)
- Use descriptive variable names
- Use local values for computed values
- Add descriptions to variables and outputs
- Use comments for complex logic

### Commit Messages

- Use the present tense ("Add feature" not "Added feature")
- Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit the first line to 72 characters or less
- Reference issues and pull requests liberally after the first line
- Consider starting the commit message with an emoji:
  - 🎨 when improving code structure/style
  - 🐛 when fixing a bug
  - ✨ when adding a new feature
  - 📚 when writing documentation
  - 🚀 when improving performance
  - ✅ when adding tests
  - 🔒 when dealing with security

## Questions?

Feel free to open an issue with the question tag or contact the maintainers directly.

## License

By contributing, you agree that your contributions will be licensed under its MIT License.
