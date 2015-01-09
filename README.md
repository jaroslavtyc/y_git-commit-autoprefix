*(author of OS-X bash compatibility is [evenh](https://github.com/evenh), thank)*

For **automatic prefixing of GIT commit messages** by JIRA (*or whatever you dream up*) issue code.

That is usable for [pairing commits at bitbucket.org with JIRA issues](https://blog.bitbucket.org/2012/04/30/linking-bitbucket-and-jira/).

***Example***

```
$ git branch
```

```
* FOO-123-bar-baz
```
 (the [JIRA project key](https://confluence.atlassian.com/display/JIRA/Defining+a+Project#DefiningaProject-Creatingaproject) is FOO)

```
$ git commit -m "qux"
```
 (commit message without any prefix)

```
$ git log
```

```
EXPOLD-123 qux
```
 (commit message has been autoprefixed by project key, **parsed from GIT branch name**)

*All the magic is made by [GIT prepare_commit_msg hook](http://git-scm.com/docs/githooks#_prepare_commit_msg)*

***Usage***

  * copy the file *hooks/prepare-commit-msg* into your own project, versioned by GIT, into project subdirectory .git/hooks
  * preserve the name of the file (prepare-commit-msg), or merge the content with existing one
  * change strings FOO, BAR, BAZ in the file to your [JIRA project key](https://confluence.atlassian.com/display/JIRA/Defining+a+Project#DefiningaProject-Creatingaproject)
  (optional: delete the unused project key strings, including trailing pipes |)
  * checkout (or create) a GIT branch in your project with name prefixed by corresponding JIRA issue (that means with preceding JIRA project key, like FOO-123-fix-user-color-settings)
  * commit something with a commit message, like "fix: used background color respects use settings"
  * look to commit history, by `git log` for example, and observe the last commit message, it should be like "FOO-123 fix: used background color respects use settings" 
