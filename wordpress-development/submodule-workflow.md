# Submodule

We use submodule to maintain our internal and external plugins. Here's the best [article](http://blogs.atlassian.com/2013/03/git-submodules-workflows-tips/) I have found so far. 

## How to roll back submodule SHA1

From time to time, especially if we have a lot of changes we might forget to not commit the SHA1. If you do already, here's the step to roll back before the PR can be merged. 

1. You would see something like this. 

![submodule conflict](https://dl.dropboxusercontent.com/u/27106646/Github-Images/Screenshot%202015-05-12%2018.40.22.png)

which you don't want it to happen in your PR. 

2. So to rollback the hash you need to go into the directory of that submodule and do `git checkout 1dba7d7ad049c06ffc7a35a6d65d4ff4098a5fcd` (according to the example above) which will checkout the previous version of the submodule. 

3. Then you can commit the change. `git add -A; git commit -m "advance submodule to previous revision"`

4. The best thing to avoid is to do `git submodule update` before anything is commiteed.
