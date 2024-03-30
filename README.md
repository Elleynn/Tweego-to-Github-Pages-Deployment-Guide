# Tweego / VS Code / GitHib Actions Practice Repository

https://elleynn.github.io/TwinePractice/

This repo demonstrates the Modern Developer's Workflow by Em Lazer-Walker. It also demonstrates compiling multiple files in the passages directory.
Copying as a template

    When copying as a template, these steps need to be done:
        Going to Settings -> Actions -> General -> Workflow permissions and:
            turning on 'Allow GitHub Actions to create and approve pull requests'
            selecting the 'Read and write permissions' option
        Going to Settings -> Secrets and variables -> Actions and creating these repository variables:
            OUTPUT_DIRECTORY with the value of dist.
            OUTPUT_FILENAME with the value of index.html.
        Going to Settings -> Pages -> Build and deployment and changing the branch to pages or whatever your publish_branch is in your workflow action peaceiris/actions-gh-pages@v3 section.

Testing changes locally
You can use mkdir -p ./dist && tweego -o ./dist/index.html ./[Insert Primary .twee Filename] then open the index.html file to view your changes.
