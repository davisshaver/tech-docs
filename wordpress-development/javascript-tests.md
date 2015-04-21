# Javascript testing

We use [Jasmine](http://jasmine.github.io/) as our testing framework and use [phantomJs](http://phantomjs.org/) for headless testing in CI. If you've followed [the frontend development guide](wordpress-development/frontend-development.md), dependicies should have been already installed via `npm install`.

## Create a simple test
Rather than providing guidelines on testable Javascript, it's easier to just show you an example how to create a test. Currently, every test sits under <code>js-tests</code> folder. Go ahead and create a test file. 

**hello-spec.js**

```javascript
describe('Hello world', function() {
    it('should say hello to me', function() {
      var hello = new Hello();
      
      expect(hello.sayHelloTo('Toy')).toBe('Hello World Toy!');
    });
});
```

Now go to your terminal and run:

```
grunt test
```

Most likely you will get something like this:

```
ReferenceError: Can't find variable: Hello
```

And that's fine because we want to do test-driven development here. Now we can fix the test by adding the function:

```javascript
var Hello = function() {

};

Hello.prototype.sayHelloTo = function(name) {
    return 'Hello World ' + name;
};
```

So the end result would be:

```javascript

var Hello = function() {

};

Hello.prototype.sayHelloTo = function(name) {
    return 'Hello World ' + name;
};

describe('Hello world', function() {
    it('should say hello to me', function() {
      var hello = new Hello();

      expect(hello.sayHelloTo('Toy')).toBe('Hello World Toy');
    });
});
```

If you run <code>grunt test</code> again, now you should see little green dots on the screen.

## Writing testable Javascript

Here's an example of how to make Javascript more easily testable.

Consider this Javascript:

```javascript
var Fusion = {
    setScheduleDay: function (day) {
        // something else up here.
        var wantedNode = $($(".show-time[data-after-eight-pm='1']:visible")[0]).closest('.schedule-show')[0];
        if (wantedNode) {
            var wantedParentNode = wantedNode.parentNode;
            var scrollToThis = (wantedNode.offsetTop - wantedParentNode.offsetTop) - 26; /* 26 is not a magic number it's the margin 25px of the div*/
            if (scrollToThis !== 0) {
                $('.schedule-day-content:visible').scrollTop(scrollToThis);
            }
        }
    }
}
```

If you have a look at the code, it's really hard to test. In _theory_, it's testable, but it would take a lot of effort. For example, you would have to inject a piece of HTML to make this code testable.

Here's how we can start from the test and make the code more easily testable.

```javascript
var Scroller = require('../../assets/js/src/lib/Scroller');

describe('When calling scroll to function', function() {

  var scroller;
  beforeEach(function() {
    scroller = new Scroller();
  });

  it('should have the correct offset and scroll to the element', function() {
    var wrapper = document.createElement('div');
    var theElement = document.createElement('div');

    wrapper.appendChild(theElement);

    var scope = $('<div></div>');
    spyOn(scope, 'scrollTop');

    scroller.within(scope).scrollTo(theElement);
    expect(scope.scrollTop).toHaveBeenCalled();
  });

});

```

And then we can refactor into another source file.

**Scroller.js**

```javascript
var Scroller = function() {
  this.scopeElement = {};
};

Scroller.prototype.within = function(scopeElement) {
  this.scopeElement = scopeElement;
  return this;
}

Scroller.prototype.scrollTo = function(targetElement) {
  var wantedNode = targetElement;
  if(wantedNode) {
    var wantedParentNode = wantedNode.parentNode;

    var scrollToThis = (wantedNode.offsetTop - wantedParentNode.offsetTop) - 26; /* 26 is not a magic number it's the margin 25px of the div*/
    if(scrollToThis !== 0) {
      this.scopeElement.scrollTop(scrollToThis);
    }
  }
};

module.exports = Scroller;

```

Then we can create another test to test the condition as well.

```javascript
it('should not do scroll effect if the element is not found', function () {
    var scope = $('<div></div>');
    spyOn(scope, 'scrollTop');
    
    scroller.within(scope).scrollTo(null);
    expect(scope.scrollTop).not.toHaveBeenCalled();
});
```

And then in the <code>theme.js</code> it would just be

```javascript
var Fusion = {
    setScheduleDay: function (day) {
        // something else up here.
        var theElement = $(".show-time[data-after-eight-pm='1']:visible").first().closest('.schedule-show')[0];
        var scopeElement = $('.schedule-day-content:visible');

        scroller.within(scopeElement).scrollTo(theElement);
    }
}
```