# Contributing to Karno

First off, thank you for considering contributing to Karno! It's people like you that make Karno such a great platform.

## Code of Conduct

This project and everyone participating in it is governed by our Code of Conduct. By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

This section guides you through submitting a bug report for Karno. Following these guidelines helps maintainers and the community understand your report, reproduce the behavior, and find related reports.

**Before creating bug reports**, please check the issue list as you might find out that you don't need to create one.

#### How Do I Submit a (Good) Bug Report?

Bugs are tracked as [GitHub issues](https://github.com/bigpapao/Karno/issues). Create an issue and provide the following information:

* **Use a clear and descriptive title** for the issue to identify the problem.
* **Describe the exact steps which reproduce the problem** in as many details as possible.
* **Provide specific examples to demonstrate the steps**.
* **Describe the behavior you observed after following the steps** and point out what exactly is the problem with that behavior.
* **Explain which behavior you expected to see instead and why.**
* **Include screenshots and animated GIFs** which show you following the described steps and clearly demonstrate the problem.

### Suggesting Enhancements

This section guides you through submitting an enhancement suggestion for Karno, including completely new features and minor improvements to existing functionality.

#### How Do I Submit a (Good) Enhancement Suggestion?

Enhancement suggestions are tracked as [GitHub issues](https://github.com/bigpapao/Karno/issues). Create an issue and provide the following information:

* **Use a clear and descriptive title** for the issue to identify the suggestion.
* **Provide a step-by-step description of the suggested enhancement** in as many details as possible.
* **Provide specific examples to demonstrate the steps**.
* **Describe the current behavior** and **explain which behavior you expected to see instead** and why.
* **Include screenshots and animated GIFs** which help you demonstrate the steps or point out the part of Karno which the suggestion is related to.
* **Explain why this enhancement would be useful** to most Karno users.

### Pull Requests

The process described here has several goals:

- Maintain Karno's quality
- Fix problems that are important to users
- Engage the community in working toward the best possible Karno
- Enable a sustainable system for Karno's maintainers to review contributions

#### Development Setup

1. Fork the repository
2. Clone your fork: `git clone https://github.com/yourusername/Karno.git`
3. Create a new branch: `git checkout -b feature/your-feature-name`
4. Install dependencies:
   ```bash
   # Backend
   cd backend
   npm install
   
   # Frontend
   cd ../frontend
   npm install
   ```
5. Make your changes
6. Test your changes
7. Commit your changes: `git commit -m 'Add some feature'`
8. Push to the branch: `git push origin feature/your-feature-name`
9. Submit a pull request

#### Pull Request Process

1. Ensure any install or build dependencies are removed before the end of the layer when doing a build.
2. Update the README.md with details of changes to the interface, this includes new environment variables, exposed ports, useful file locations and container parameters.
3. Increase the version numbers in any examples files and the README.md to the new version that this Pull Request would represent.
4. You may merge the Pull Request in once you have the sign-off of two other developers, or if you do not have permission to do that, you may request the second reviewer to merge it for you.

## Styleguides

### Git Commit Messages

* Use the present tense ("Add feature" not "Added feature")
* Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
* Limit the first line to 72 characters or less
* Reference issues and pull requests liberally after the first line
* Consider starting the commit message with an applicable emoji:
    * 🎨 `:art:` when improving the format/structure of the code
    * 🐎 `:racehorse:` when improving performance
    * 🚱 `:non-potable_water:` when plugging memory leaks
    * 📝 `:memo:` when writing docs
    * 🐧 `:penguin:` when fixing something on Linux
    * 🍎 `:apple:` when fixing something on macOS
    * 🏁 `:checkered_flag:` when fixing something on Windows
    * 🐛 `:bug:` when fixing a bug
    * 🔥 `:fire:` when removing code or files
    * 💚 `:green_heart:` when fixing the CI build
    * ✅ `:white_check_mark:` when adding tests
    * 🔒 `:lock:` when dealing with security
    * ⬆️ `:arrow_up:` when upgrading dependencies
    * ⬇️ `:arrow_down:` when downgrading dependencies
    * 👕 `:shirt:` when removing linter warnings

### JavaScript Styleguide

All JavaScript must adhere to [JavaScript Standard Style](https://standardjs.com/).

* Prefer the object spread operator (`{...anotherObj}`) to `Object.assign()`
* Inline `export`s with expressions whenever possible
  ```javascript
  // Use this:
  export default class ClassName {

  }

  // Instead of:
  class ClassName {

  }
  export default ClassName
  ```

### CSS Styleguide

* Use Tailwind CSS classes whenever possible
* Follow BEM methodology for custom CSS classes
* Use kebab-case for CSS class names

## Additional Notes

### Issue and Pull Request Labels

This section lists the labels we use to help us track and manage issues and pull requests.

#### Type of Issue and Issue State

* `enhancement` - Feature requests.
* `bug` - Confirmed bugs or reports that are very likely to be bugs.
* `question` - Questions more than bug reports or feature requests (e.g. how do I do X).
* `feedback` - General feedback more than bug reports or feature requests.
* `help-wanted` - The Karno core team would appreciate help from the community in resolving these issues.
* `beginner` - Less complex issues which would be good first issues to work on for users who want to contribute to Karno.
* `more-information-needed` - More information needs to be collected about these problems or feature requests.
* `needs-reproduction` - Likely bugs, but haven't been reliably reproduced.
* `blocked` - Issues blocked on other issues.
* `duplicate` - Issues which are duplicates of other issues.
* `wontfix` - The Karno core team has decided not to fix these issues for now.
* `invalid` - Issues which aren't valid (e.g. user errors).

Thank you for contributing to Karno! 🚗✨