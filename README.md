# How to Publish Twine Games to Your GitHub Page

### What is **Twine**?

Twine is a free, open-source application used to create interactive fiction. For more information, visit the [official Twine website](https://twinery.org/).

### What is **Twee**?

Twee is the [source code of a Twine story](https://twinery.org/cookbook/terms/terms_twee.html).

### What is **Tweego**?

Tweego is a free command line interface compiler for Twine/Twee projects, written in Go. Tweego allows users to write (and compile) their Twine projects in their preferred text editor. See further documentation at the [official website](https://www.motoslave.net/tweego/) or on the [project's Github repository](https://github.com/tmedwards/tweego).

## Introduction

In early 2024, I started coding all of my Twine projects in a plain text file using VS Code, Tweego, and a [Twee3 syntax highlighting extension](https://marketplace.visualstudio.com/items?itemName=cyrusfirheir.twee3-language-tools) from the marketplace. My reasons for doing so can largely be attributed to the word that haunts all developers: Scalability. I am very fond of the Twine application - but larger works are a nightmare to keep track of in the visual node-based software.

A large part of this project takes inspiration from Em Lazer-Walker's _[A Modern Developer's Workflow For Twine](https://dev.to/lazerwalker/a-modern-developer-s-workflow-for-twine-4imp)_ and 6note's [TweeExample Repo](https://github.com/6notes/tweeExample). Certain portions of these tutorials have depreciated since initial publication, so I have created an alternative workflow that instead grabs a precompiled zip of Tweego to use in the build process. 

So what's the difference? When I created this repository, I noticed Tweego had compatibility issues with more recent versions of GO that included [Modules](https://go.dev/blog/using-go-modules) (V1.11.+) and trying to compile Tweego in the build process was a bit... [Finnicky](https://github.com/6notes/tweeExample/pull/1). I experimented with various GO versions and disabling `GO111MODULE` with some success, but ultimately decided that using a precompiled zip suited my needs just fine and sidestepped any issues of GO compatibility entirely. Additionally, the main branch of the Tweego repo updates very infrequently - so the chance of the precompiled download of Tweego being different from the project's main branch is very small.

## What Does This Repository Do?

This repository is meant to serve as an example on how to set up GitHub Actions (`build.yml` in the `.github/workflows` directory) in order to compile multiple Twee files (found in the `src` directory of the `main` branch) and deploy the resulting HTML file to a custom domain (or a GitHub Page). I highly recommend utilizing this repository in conjunction with the [guide I mentioned previously](https://dev.to/lazerwalker/a-modern-developer-s-workflow-for-twine-4imp) if you do not already have Go and Tweego installed.

You can see the compiled result of this repository at [www.TwinePractice.ElleYnn.com](https://www.twinepractice.elleynn.com/).

## Workflow Setup

### Step 1: Configure Workflow Permissions

Before using the provided `build.yml` file, make sure your GitHub Actions are configured with the appropriate permissions:

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
   
***Keep in mind the expiration date you have chosen for your token. If your token expires, your builds will all fail. Fortunately, the solution is as simple as regenerating the token.***

### Step 4: Add the Personal Access Token to Your Repository Secrets

Add your GitHub Personal Access Token to your repository secrets:

1. Go to your repository's `Settings` > `Secrets and variables` > `Actions`.
2. Click `New repository secret`.
3. Name the secret `PERSONAL_TOKEN` and paste your PAT into the value field.
4. Click `Add secret`.

### Step 5: Customize the `build.yml` File

Adjust the `build.yml` file as needed. Set the `cname` field to your custom domain if applicable, or remove the line if not using a custom domain.

## Using the Workflow

Once everything is configured, any push/commit to the `main` branch will trigger the build and deployment of your project. Your game will be built using the precompiled version of Tweego and published to GitHub Pages.

## FAQ

### Can I fork this repo and do my own thing?

Totally.

### Do I HAVE to use repository variables?

No. I won't tell anyone.

### Do you know how to do XYZ in Harlowe/SugarCube/Snowman/etc?

Probably not. If documentation I've listed above doesn't do it for you, then you should definitely check out [r/TwineGames](https://www.reddit.com/r/twinegames/) and the [associated discord](https://discord.com/invite/n5dJvPp). The [Twine forum](https://twinery.org/forum/) is Read-Only now, but still has a lot of good information. In addition, the [Interactive Fiction forum](https://intfiction.org/c/authoring/twine) has a section dedicated to Twine that is fairly robust.

### Can ChatGPT/Claude/DeepSeek/Mistral/CoPilot/AI help me with my code?

Eh, I personally don't think any of the AI models are worth it. These programs essentially function as super fancy (and super expensive) predictive text - they don't actually _understand_ your questions. You _might_ get a working code snippet back, but more likely than not you'll get back a code snippet that only _looks_ like it works. I suggest sticking with real people in one of the forums. They might _also_ give you bad code - but fighting a real person is a lot more satisfying than trying to argue with a chatbot.

## Further Assistance

If you encounter any issues or need further assistance, please refer to the [GitHub Actions documentation](https://docs.github.com/en/actions) or raise an issue in this repository.

