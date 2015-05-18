# Submodule

We use submodule to maintain our internal and external plugins. Here's the best [article](http://blogs.atlassian.com/2013/03/git-submodules-workflows-tips/) I have found so far of git submodule workflow. Also, [What is git submodule?](http://git-scm.com/book/en/v2/Git-Tools-Submodules) is also a nice article to start with.

## How to roll back submodule SHA1

From time to time, especially if we have a lot of changes we might forget to not commit the SHA1. If you do already, here's the step to roll back before the PR can be merged. 

1. You would see something like this. 

![screenshot 2015-05-12 18 40 22](https://cloud.githubusercontent.com/assets/638379/7600363/6e8d94bc-f8d8-11e4-910a-d03abe6b8a2c.png)

which you don't want it to happen in your PR. 

2. So to rollback the hash you need to go into the directory of that submodule and do `git checkout 1dba7d7ad049c06ffc7a35a6d65d4ff4098a5fcd` (according to the example above) which will checkout the previous version of the submodule. 

3. Then you can commit the change in your main directory that contains the submodule you just rolled back. `git add -A; git commit -m "advance submodule to previous revision"`.

4. Then you can push the change `git push origin <your branch name>`

### Note
The best thing to avoid is to do `git submodule update` before anything is commiteed.

## What can you do to prevent this to happen

1. You can do checkout and update submodule in the same time. `git pull origin master && git submodule update`

2. You can ignore the whole submodule directory by doing this `git update-index --assume-unchanged <the directory you want to ignore>/*`

3. You can create custom shell function to checkout a branch and update submodules in the same time 

```
function go {
    git checkout $1 && git submodule update
}
```

So when you want to checkout a branch you can just do `go master`

## GIT Gui
Unfortunetely, there's no way to do this in Github for OsX. You have to do this manually.

## Summary

All of this just some examples that you can do to avoid the headache. The most important thing is to pay attention to what you are committing but if you made a mistake which we are all then you can roll back by the steps above. 
