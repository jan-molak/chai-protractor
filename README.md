# Chai Smoothie - Protractor assertions for Chai

[Chai Smoothie](https://github.com/jan-molak/chai-smoothie) smooths out the sharp angles of your
[Protractor](https://github.com/angular/protractor)-powered automated web tests.


The library provides a set of custom
[Chai](http://chaijs.com/)
assertions to help your Protractor-based [Serenity/JS](https://github.com/jan-molak/serenity-js) tests
express their intent better, give assertion errors more meaning,
and reduce the amount of time your team spends troubleshooting the failures.

Chai Smoothie comes with [TypeScript](https://www.typescriptlang.org/) typings
and works with [Chai-as-Promised](https://github.com/domenic/chai-as-promised),
[Serenity/JS](https://github.com/jan-molak/serenity-js),
and plain [Protractor](https://github.com/angular/protractor) tests too!

---

To add Chai Smoothie to your [Node.js](https://nodejs.org/) project:

```
npm install chai-smoothie --save-dev
```

---

## The Motivation and The (Missing) Context

Let's assume that we'd like to find out a bit more about the state of an HTML element defined as:

``` html
<h1 id="title">Chai Smoothie is delicious!</h1>
```

A [typical approach](http://goo.gl/Zrk4Vj) used in Protractor tests
to check if an element is displayed looks more or less like this:

```typescript
expect(element(by.id('title')).isDisplayed()).to.eventually.be.true
```

When the element identified by the id of "`title`" is displayed, the assertion works fine and won't bother us.

However, should the element decide to _not_ appear, the assertion will fail telling us that:

```
AssertionError: expected false to be true
```

Although Chai is doing its best to tell us the reason of the failure,
the only information it has available with this approach is the boolean state of element's visibility.
This lack of context is what causes the error message to not be particularly useful.

Chai Smoothie gives Chai the missing context and makes the assertion more readable too!

### Vanilla Protractor

If your automated web tests use Protractor, you can use Chai Smoothie to turn the assertion from the previous example
into something a bit more readable:

```typescript
expect(element(by.id('title'))).to.eventually.be.displayed
```

Should the above assertion fail, the error message we'll see will present more context:

```
AssertionError: Expected the element located By(css selector, *[id="title"]) to be displayed, but it's not.
```

### Serenity/JS

Since [Serenity/JS](https://github.com/jan-molak/serenity-js) builds on the shoulders of Protractor,
you can use similar syntax with
[Serenity/JS Questions](https://github.com/jan-molak/serenity-js/blob/master/docs/screenplay-pattern.md#question):

```typescript
expect(actor.toSee(Article.Title)).displayed
```

Using the open-source Serenity/JS library has other benefits too - [learn more](https://github.com/jan-molak/serenity-js).

## Setting up

Install [Chai](http://chaijs.com/):

```
npm install chai --save-dev
```

Install Chai Smoothie:

```
npm install chai-smoothie --save-dev
```

### TypeScript

```typescript
import chai = require('chai');
chai.use(require('chai-smoothie'));
const expect = chai.expect;

expect(element(by.css('h1'))).to.be.present;
```

### JavaScript

```javascript
var chai = require('chai');
chai.use(require('chai-smoothie'));
var expect = chai.expect;

expect(element(by.css('h1'))).to.be.present;
```


## Available Assertions

Chai Smoothie provides following assertions, each of which can be:
* negated using the `not` operator: `expect(el).not.to.be.displayed`, `expect(el).not.to.be.present.eventually`, etc.
* used in conjunction with [chai-as-promised](https://github.com/domenic/chai-as-promised),
to highlight that the Chai Smoothie assertions return promises: `return expect(el).to.eventually.be.present`.

| Assertion | Example                      | Meaning                                           | Protractor API |
| ---       | ---                          | ---                                               | ---            |
| displayed | `expect(el).to.be.displayed` | An element exists in the DOM and is visible      | [`isDisplayed()`](http://www.protractortest.org/#/api?view=webdriver.WebElement.prototype.isDisplayed) |
| enabled   | `expect(el).to.be.enabled`   | A form control element, such as an `input`, is [not disabled](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-disabled)  | [`isEnabled()`](http://www.protractortest.org/#/api?view=webdriver.WebElement.prototype.isEnabled) |
| present   | `expect(el).to.be.present`   | An element exists in the DOM, but can be hidden  | [`isPresent()`](http://www.protractortest.org/#/api?view=webdriver.WebElement.prototype.isPresent) |
| selected  | `expect(el).to.be.selected`  | A form control, such as an `input` `checkbox` is [checked](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-checked) | [`isSelected()`](http://www.protractortest.org/#/api?view=webdriver.WebElement.prototype.isSelected) |

## Getting Help

To ask about the usage and troubleshooting of Serenity/JS or any of its components, such as Chai Smoothie,
[post a **serenity-js** tagged question on StackOverflow](http://stackoverflow.com/questions/tagged/serenity-js).

## Your feedback matters!

Do you find Chai Smoothie useful? Give it a star! &#9733;

Found a bug? Need a feature? Raise [an issue](https://github.com/jan-molak/chai-smoothie/issues?state=open)
or submit a pull request.

Have feedback? Let me know on twitter: [@JanMolak](https://twitter.com/JanMolak)

## License

The Chai Smoothie library is licensed under the [Apache-2.0](LICENSE.md) license.

If you're interested in a commercial license, training, support or bringing your team up to speed with modern software
development practices - [please get in touch](https://janmolak.com/about-the-author-e45e048661c#.kxqp57qn9).
