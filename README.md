## Tweego / VS Code / GitHub Actions Practice Repository

See the compiled result of this repository at [www.TwinePractice.ElleYnn.com](https://www.twinepractice.elleynn.com/).

This repo demonstrates compiling multiple Twine files in the `src` directory of the `main` branch and deploying the HTML file to a custom domain (or a GitHub Page) via a GitHub Actions workflow.

A large part of this project takes inspiration from Em Lazer-Walker's ['A Modern Developer's Workflow For Twine'](https://dev.to/lazerwalker/a-modern-developer-s-workflow-for-twine-4imp) and 6note's [TweeExample repository](https://github.com/6notes/tweeExample). Certain portions of these examples have depreciated since their publication, so I have created an alternative workflow that does not use the Go Environment since Tweego does not currently support Go modules. Instead, this workflow uses [jq for JSON processing](https://jqlang.github.io/jq/manual/) and the GitHub API to grab the latest precompiled version of Tweego.

## Workflow Setup

### Step 1: Configure Workflow Permissions

Before using the provided `build.yaml` file, make sure your GitHub Actions are configured with the appropriate permissions:

1. Navigate to your repository on GitHub.
2. Go to `Settings` > `Actions` > `General`.
3. Under **Workflow permissions**, make sure the following are set:
   - Turn on 'Allow GitHub Actions to create and approve pull requests'.
   - Select the 'Read and write permissions' option.

### Step 2: Set Repository Variables

Set up the necessary repository variables for your GitHub Actions workflow:

1. Go to your repository's `Settings` > `Secrets and variables` > `Actions`.
2. Create the following repository variables:
   - `OUTPUT_DIRECTORY`: Set this to `dist` (or your preferred output directory for the compiled game).
   - `OUTPUT_FILENAME`: Set this to `index.html` (or your preferred name for the compiled game file).

### Step 3: Add a GitHub Personal Access Token

Create a GitHub Personal Access Token (PAT) to allow your workflow to authenticate with the GitHub API:

1. Visit [GitHub Personal Access Tokens](https://github.com/settings/tokens) page and log in to your account.
2. Click `Generate new token`.
3. Provide a descriptive name for your token.
4. Under scopes, select `public_repo` if your repository is public. Adjust scopes as needed for private repositories.
5. Click `Generate token`.
6. Copy the generated token.

### Step 4: Add the Personal Access Token to Your Repository Secrets

Add your GitHub Personal Access Token to your repository secrets:

1. Go to your repository's `Settings` > `Secrets and variables` > `Actions`.
2. Click `New repository secret`.
3. Name the secret `PERSONAL_TOKEN` and paste your PAT into the value field.
4. Click `Add secret`.

### Step 5: Customize the `build.yaml` File

Adjust the `build.yaml` file as needed. Set the `cname` field to your custom domain if applicable, or remove the line if not using a custom domain.

## Using the Workflow

Once set up, any push to the `main` branch will trigger the build and deployment of your project. Your game will be built using the latest version of Tweego and published to GitHub Pages.

## Further Assistance

If you encounter any issues or need further assistance, please refer to the [GitHub Actions documentation](https://docs.github.com/en/actions) or raise an issue in this repository.

