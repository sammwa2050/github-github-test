Import your project from GitHub to GitLab
Tier: Free, Premium, Ultimate
Offering: GitLab.com, GitLab Self-Managed, GitLab Dedicated
History 
You can import your GitHub projects from either GitHub.com or GitHub Enterprise. Importing projects does not migrate or import any types of groups or organizations from GitHub to GitLab.

Imported issues, merge requests, comments, and events have an Imported badge in GitLab.

The namespace is a user or group in GitLab, such as gitlab.com/sidney-jones or gitlab.com/customer-success.

Using the GitLab UI, the GitHub importer always imports from the github.com domain. If you are importing from a self-hosted GitHub Enterprise Server domain, use the GitLab Import API GitHub endpoint.

You can change the target namespace and target repository name before you import.

 For an overview of the import process, see How to migrate from GitHub to GitLab including Actions.

Estimating import duration
Every import from GitHub is different, which affects the duration of imports you perform. However, in our testing we imported https://github.com/kubernetes/kubernetes in 76 hours. When we tested, that project comprised:

80,000 pull requests.
45,000 issues.
Approximately 1.5 million comments.
Prerequisites
To import projects from GitHub, you must enable the GitHub import source. If that import source is not enabled, ask your GitLab administrator to enable it. The GitHub import source is enabled by default on GitLab.com.

Permissions and roles
History 
To use the GitHub importer, you must have:

Access to the GitHub project to import.
At least the Maintainer role on the destination GitLab group to import to.
Also, the organization the GitHub repository belongs to must not impose restrictions of a third-party application access policy on the GitLab instance you import to.

Accounts for user contribution mapping
History 
Before using the old method of user contribution mapping for imports to GitLab Self-Managed and GitLab Dedicated, you must meet certain requirements. Imports to GitLab.com use an improved method that doesn’t require preparation.

These requirements are:

Each GitHub author and assignee in the repository must have a public-facing email address.
The GitHub user’s email address must match their GitLab email address.
If a user’s email address in GitHub is set as their secondary email address in GitLab, they must confirm it.
GitHub Enterprise does not require a public email address, so you might have to add it to existing accounts.

Known issues
GitHub pull request comments (known as diff notes in GitLab) created before 2017 are imported in separate threads. This occurs because of a limitation of the GitHub API that doesn’t include in_reply_to_id for comments before 2017.

Because of a known issue, Markdown attachments from repositories on GitHub Enterprise Server instances aren’t imported.

Because of a known issue, when importing projects that used GitHub auto-merge, the imported project in GitLab can have merge commits labeled unverified if the commit was signed with the GitHub internal GPG key.

GitLab can’t import GitHub Markdown image attachments that were uploaded to private repositories before 2023-05-09. If you encounter this problem, would like to help us resolve the problem, and are willing to provide a sample repository for us, please add a comment to issue 424046 and we’ll contact you.

For GitLab-specific references, GitLab uses the # character for issues and a ! character for merge requests. However, GitHub uses only the # character for both issues and pull requests. When importing:

Comment notes, GitLab only creates links to issues because GitLab can’t determine whether a references points to an issue or a merge request.
Issues or merge request descriptions, GitLab doesn’t create links for any references because their imported counterparts might not have been created on the destination yet.
Import your GitHub repository into GitLab
You can import your GitHub repository by either:

Using GitHub OAuth
Using a GitHub personal access token
Using the API
If importing from github.com you can use any method to import. Self-hosted GitHub Enterprise Server customers must use the API.

Use GitHub OAuth
If you are importing to GitLab.com or to a GitLab Self-Managed that has GitHub OAuth configured, you can use GitHub OAuth to import your repository.

This method has an advantage over using a personal access token (PAT) because the backend exchanges the access token with the appropriate permissions.

On the left sidebar, at the top, select Create new (  ) and New project/repository.
Select Import project and then GitHub.
Select Authorize with GitHub.
Proceed to selecting which repositories to import.
To use a different method to perform an import after previously performing these steps, sign out of your GitLab account and sign in again.

Use a GitHub personal access token
To import your GitHub repository using a GitHub personal access token:

Generate a GitHub personal access token. Only classic personal access tokens are supported.
Go to https://github.com/settings/tokens/new.
In the Note field, enter a token description.
Select the repo scope.
Optional. To import collaborators, or if your project has Git LFS files, select the read:org scope.
Select Generate token.
On the GitLab left sidebar, at the top, select Create new (  ) and New project/repository.
Select Import project and then GitHub.
Select Authorize with GitHub.
In the Personal access token field, paste the GitHub personal access token.
Select Authenticate.
Proceed to selecting which repositories to import.
To use a different token to perform an import after previously performing these steps, sign out of your GitLab account and sign in again, or revoke the older token in GitHub.

Use the API
The GitLab REST API can be used to import a GitHub repository. It has some advantages over using the GitLab UI:

Can be used to import GitHub repositories that you do not own if they are public.
It can be used to import from a GitHub Enterprise Server that is self-hosted.
Can be used to set the timeout_strategy option that is not available to the UI.
The REST API is limited to authenticating with GitLab personal access tokens.

To import your GitHub repository using the GitLab REST API:

Generate a GitHub personal access token. Only classic personal access tokens are supported.
Go to https://github.com/settings/tokens/new.
In the Note field, enter a token description.
Select the repo scope.
Optional. To import collaborators, or if your project has Git LFS files, select the read:org scope.
Select Generate token.
Use the GitLab REST API to import your GitHub repository.
