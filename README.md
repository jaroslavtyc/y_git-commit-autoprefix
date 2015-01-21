For **automatic prefixing of GIT commit messages** by JIRA (*or whatever you dream up*) issue code.

That is suitable for [pairing commits at bitbucket.org with JIRA issues](https://blog.bitbucket.org/2012/04/30/linking-bitbucket-and-jira/).

##### [*Example*](#example)
##### [*Usage*](#usage)
##### [*Hints*](#hints)


#### *Example*

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

*All the magic is made by [GIT commit_msg hook](http://git-scm.com/docs/githooks#_commit_msg)*

### *Usage*

*[Master branch](/jaroslavtyc/git-commit-autoprefix/tree/master) is for __Linux__ bash format. For OSX use the [osx-compatible branch](/jaroslavtyc/git-commit-autoprefix/tree/osx-compatible) instead.*

  * copy the file *hooks/commit-msg* into your own project, versioned by GIT, into project subdirectory .git/hooks
  * preserve the name of the file (commit-msg), or merge the content with existing one
  * change strings FOO, BAR, BAZ in the file to your [JIRA project key](https://confluence.atlassian.com/display/JIRA/Defining+a+Project#DefiningaProject-Creatingaproject)
  (optional: delete the unused project key strings, including trailing pipes |)
  * checkout (or create) a GIT branch in your project with name prefixed by corresponding JIRA issue (that means with preceding JIRA project key, like FOO-123-fix-user-color-settings)
  * commit something with a commit message, like "fix: used background color respects use settings"
  * look to commit history, by `git log` for example, and observe the last commit message, it should be like "FOO-123 fix: used background color respects use settings" 

### *Hints*

Did you know you can share same GIT branch with more JIRA issues?
  * just prefix the branch name by issue codes, like FOO-123-BAR-789-baz
  * the hook will take care about proper prefixing of your commits (since commit ad93fcaaa7f199617f5ca7839849c9668266d221, 2015-01-20)
