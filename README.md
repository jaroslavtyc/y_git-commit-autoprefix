For automatic prefixing of GIT commit messages by JIRA (or whatever you dream up) issue code.
That is usable for pairing commits at bitbucket.org with JIRA.

Example:

```
$ git branch
```

```
$ ...
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
$ ...
   EXPOLD-123 qux
```
 (commit message has been autoprefixed by project key, parsed from GIT branch name)

*All the magic is made by [GIT prepare_commit_msg hook](http://git-scm.com/docs/githooks#_prepare_commit_msg)*

***Usage***

  * copy the file prepare-commit-msg into your own project, versioned by GIT, into project subdirectory .git/hooks
  * preserve the name of the file (prepare-commit-msg), or merge the content with existing one
  * change strings FOO, BAR, BAZ to your [JIRA project key](https://confluence.atlassian.com/display/JIRA/Defining+a+Project#DefiningaProject-Creatingaproject)
  (if you have just single one, delete the other strings, including the pipe |)
  * checkout (or create) a GIT branch in your project with name prefixed by corresponding JIRA issue (with preceding JIRA project key, like FOO-123-fix-user-color-settings)
  * commit something with some commit message, like "fix: used background color respects use settings"
  * look to commit history, by `git log` for example, at observe the last commit message, it should be like "FOO-123 fix: used background color respects use settings" 
