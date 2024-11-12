# Github

This page goes over the best practices on how we use github to manage our project and workflow.

## Semantic Commit Messages
We use semantic commit messages to keep our commit history clean, organized, and easy to understand. This helps us quickly identify what each commit does, track down issues, and generate meaningful release notes.

### Commit Message Format
A semantic commit message follows this format:
```php
<type>(<scope>): <description>
```

#### Type: The type of change being made (e.g., feat, fix, docs, style, refactor, test, chore).
#### Scope (optional): The scope of the change (e.g., variable name, file, module, feature).
#### Description: A short description of the change.


### Examples
Here are some examples of semantic commit messages:
```php
feat(cart): add functionality to apply discount codes
fix(login): resolve session timeout issue on login page
docs(readme): update setup instructions for developers
style(product-list): format product cards for mobile view
refactor(api): simplify order processing logic for scalability
test(user): add unit tests for user registration process
chore(env): configure dotenv for environment variables
```

## Pull Request Guidelines
When creating a pull request, follow these guidelines to ensure your code is reviewed and merged smoothly.

### Pull Request Template
Use the following template when creating a pull request:

```php
## Description
Describe the changes made in this pull request. Explain what feature, bug fix, or enhancement was added, and why it was necessary. Provide any context that will help reviewers understand the purpose of the PR.

## Related Issue(s)
Link any related issues here by using "Closes #issue-number". If this PR resolves multiple issues, list each one.

## Type of Change
- [ ] 🆕 New feature (adds functionality to the webshop app)
- [ ] 🐛 Bug fix (resolves an issue in the webshop app)
- [ ] 🔄 Refactor (improves code structure without changing functionality)
- [ ] 🔧 Chore (maintenance task, e.g., updating dependencies)

## Checklist
- [ ] My code follows the code style and conventions of the project.
- [ ] I have performed a self-review of my code.
- [ ] I have commented my code, particularly in hard-to-understand areas.
- [ ] I have written unit tests for the changes, if necessary.
- [ ] All tests pass on my local machine.
- [ ] This PR is ready for review.

## Additional Notes
Add any additional information here. Mention if there are any known issues, limitations, or special considerations for the PR.
```
