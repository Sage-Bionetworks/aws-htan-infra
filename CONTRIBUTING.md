# Contribution Guidelines

For more information on how this repository was set up, check out this [**Confluence page**](https://sagebionetworks.jira.com/wiki/spaces/IT/pages/2058878986) on how to bootstrap AWS accounts.

## Setting up the repository for development

1. Install [pipenv](https://pipenv.pypa.io/en/latest/install/#installing-pipenv) and the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) (version 2).

2. Create an isolated Python virtual environment using `pipenv` after cd'ing into the repository's directory.

   ```
   pipenv install --dev
   ```

3. Install the pre-commit hooks into Git to lint files before commiting changes.

   ```
   pipenv run pre-commit install
   ```

4. Create an IAM user with programmatic access using the AWS Management Console accessible via JumpCloud.

5. Configure a profile with the AWS CLI.

   ```
   aws configure --profile <aws_profile>
   ```

## Testing sceptre deployment

You can test the deployment of a stack group and then delete the resulting resources using the following commands:

```
# Activate the pipenv virtual environment to use sceptre
pipenv shell

# Test the deployment of the 'prod' stack group
sceptre --var "profile=<aws_profile>" launch --yes prod

# Delete the test deployment of the 'prod' stack group
sceptre --var "profile=<aws_profile>" delete --yes prod
```

**N.B.** If your text editor (_e.g._ Visual Studio Code) or shell (_e.g._ using [`direnv`](https://direnv.net/)) can automatically activate the `pipenv` virtual environment, you can omit the `pipenv shell` command.

## Updating Pipfile

If you need to add a Python dependency or bump a package version, you need to manually edit the Pipfile accordingly and run the following command to update the associated `Pipfile.lock` with the corresponding versions and hashes.

```
pipenv update
```
