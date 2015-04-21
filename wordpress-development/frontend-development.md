# Frontend Development

We use [Grunt](http://gruntjs.com/getting-started) as our build sytem for compiling SASS and Javascript, and running various tests/linting functions.

1. Make sure you have [Grunt](http://gruntjs.com/getting-started) installed globally.
1. Go to your theme directory and install the necessary libraries using <code>npm install</code>
1. Voilà! Run <code>grunt watch</code> in your terminal and leave it there. It will watch your change and recompile everything for you. You should see something like this.

```
Running "watch" task

Waiting...
```

### Pro tip: Compile before you commit

Please make sure that you've run <code>grunt</code> in your theme folder prior to committing a change in styling or script. Right now our continuous integration doesn't run the command automatically and deploy updated assets, so we have to compile manually.