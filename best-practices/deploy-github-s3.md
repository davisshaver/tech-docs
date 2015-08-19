# Deploying a Github repo to Amazon S3

Have some static or built assets stored in Github that you'd like to have deployed to Amazon S3?

You're in luck! Travis CI [supports S3 as a deployment destination](http://docs.travis-ci.com/user/deployment/s3/).

Before you begin, you'll need to add Travis CI to your repo. The easiest way to do this is from your [Travis profile page](https://magnum.travis-ci.com/profile/fusioneng).

Here are some additional helpful tips to follow:

**1. Limit deploys to master branch builds**

```yml
deploy:
  provider: s3
  [...]
  on:
    branch: master
```

**2. Skip the actual build process if your code is already built / compiled**

```yml
install: echo 'skip install'
script: echo 'skip build'
```

**3. Amazon IAM (capability management) is a pain. You will probably spend the most time getting details correct.**

**4. Reduce the noisyness of your email notifications.**

```yml
notifications:
  on_success: never
  on_failure: change
```
**5. Add the Travis chicklet to your README.md for easy access to the build log**

If you've successfully followed the configuration instructions, Travis will automatically push each build to S3.
