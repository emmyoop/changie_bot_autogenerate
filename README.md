# changie_bot_autogenerate

### Description
When using [changie](https://changie.dev/) to generate your changelog, it is useful to be able to autogenerate a changelog file in the format expected by changie when a bot creates a PR.  This action creates a new yaml file, commit it with a specified bot and then the commit will be pushed to the PR.

A common use is PRs created by dependabot.

#### Why
Automate changelog generation for more visability with automated bot changes.

#### When
Once a PR is created and it has been labeled as indicated.  It will only create a new yaml file if none already exists on the PR.  

An exampe use is for PRs created by dependabot.  You can also manually trigger this by adding the specified label at any time.

#### Required inputs

- `GITHUB_TOKEN`: If you expect the resulting commit to add a changelog should retrigger workflows, you will need to use a Personal Access Token for the bot to commit the file.  When using the GITHUB_TOKEN, the resulting commit will not trigger another GitHub Actions Workflow run. This is due to limitations set by GitHub. See [the docs](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#using-the-github_token-in-a-workflow).
- `commit_author`: Author of the commit for the changelog file. Author expected in the format "Lorem J. Ipsum <lorem@example.com>"
- `changie_kind`: Type of changelog file  # TODO: how does changie define this?
- `label`: GitHub label to trigger off

#### Optional inputs

- `commit_message`:
    - description: Message to put on commit of new changelog file
    - default: "Add automated changelog yaml from template"
- `custom_changelog_string`: # is this the right way?  could it be templated? start here and iterate.
    - description: The multi-line string containg the expected contents of the custom fields for a changelog entry.

### Assumptions

1. You're using changie
2. Your changelogs live in the default `.changes. path, nothing custom
3. This action is called in the context of a PR
4. Not changelog yaml file already exists on this PR
5. This PR already exists and you just need to add a commit with the changelog to it