# Self-hosted Runner

GitHub self-hosted runners play a crucial role in:

- Kicking off deployment processes and accessing necessary virtual machines.
- Executing GitHub Actions workflows, especially when GitHub-hosted runners fall short.

## Authenticating Self-hosted Runners

Proper authentication is key. Avoid using personal access tokens for setting up self-hosted runners due to security
risks. Instead, opt for GitHub Apps, offering a more secure alternative.

<div class="warning">

**Important: Avoid Personal Access Tokens**

Personal Access Tokens are linked to individual users, posing security risks if compromised. They often come with
excessive privileges, leading to increased risk. Additionally, they require creating service accounts (resulting in
additional license consumption) and are less secure compared to GitHub applications.

</div>

### Creating a GitHub Application

1. Go to your GitHub organization: Settings -> Developer Settings -> GitHub Apps -> New GitHub app.
2. Enter the application name (e.g., `BIIP Workflows Self-hosted Runner`).
3. Provide any homepage URL.
4. Uncheck the "active" option for WebHooks.

#### Permissions

Choose between repository-scoped or organization-scoped runners. Set the following required permissions:

**For Repository Runners:**

- Actions (read)
- Administration (read/write)
- Checks (read) (if using Webhook Driven Scaling)
- Metadata (read)

**For Organization Runners:**

- Actions (read)
- Metadata (read)

**Organization Permissions:**

- Self-hosted runners (read/write)

#### Private Key

Download the private key file by clicking "Generate a private key" at the bottom of the GitHub App page. This file will
be used later in the installation process.

#### Installation

1. Go to the "Install App" tab on the left side of the page.
2. Install the GitHub App you created for your organization.
3. Select the repositories where you want to install the GitHub app and use self-hosted runners.

<div class="warning">

**Important: Avoid Installing Self-hosted Runners on Public Repositories**

GitHub recommends using self-hosted runners exclusively with private repositories. Public repository forks could
potentially execute malicious code on your self-hosted runner machine through pull requests. For more information, refer
to [GitHub's documentation](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners).

</div>

# Credits

- Permissions list is based
  on [ocpdude/actions-runner-controller](https://github.com/ocpdude/actions-runner-controller/blob/main/README.md)
  documentation.
