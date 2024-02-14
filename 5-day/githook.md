# What are git hooks?
Git hooks are shell scripts that trigger when we perform a specific action in `git`.
They are useful tools for automating text as we move through our general `workflow`. 

We can trigger `git hooks` around specific `git actions`. For example, we can set up a 
`git hook` that prevents we from committing if the `hook script` detects problem. 

`git hook` exists as simple text files in our `.git/hooks` directory. 
If we just initialize the repo there will be a `.git` folder in our repository. 

If we do not see this folder we will need to make sure we can see hidden folders on our operating system first.

# Types of Git Hooks
There are two main types of git hooks:

- __Client-side hooks__ - Run on our local machine
- __Server-side hooks__ - Run on the Git server

Some examples of client-side hooks include:

`pre-commit` - Runs before we commit

`post-commit`- Runs after we commit

`pre-push` - Runs before we push

`post-merge` - Runs after a merge


### How to Use Git Hooks
To use a git hook, simply create an executable script in the `.git/hooks` directory with the name of the hook we want to trigger.

__For example:__

```shell
#!/bin/sh
# .git/hooks/pre-commit

echo "Running pre-commit hook"
```


Make sure to make the script executable by running `chmod +x hook-script.sh`.

Now this script will run every time before we commit. We can add any logic we want to these scripts to automate workflows.

Git hooks are powerful tools to optimize and automate our development process.