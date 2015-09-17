
# web端自动化测试分享-广发前端小伙伴

## 内容概要：

> 常用的前端测试框架介绍 （Jasmine Mocha Qunit 它们各自的特点）

> Jasmine 自动化测试3种方式 （1.pure Jasmine 2.work with Karma and gulp/grunt 3.build in webStorm）

> Jasmine 自动化测试举例 （work with Angular）

> What is TDD and how to TDD

> 添加自动化测试的好处

#### 前言
	所有自动化测试遵循3个步骤：
	1.Describe what you're going to test
	2.Set up the precondition
	3.do the Assertion (Does result match your expectation)

#### 常用的前端框架
- 1.[QUnit](http://qunitjs.com/) 

>QUnit is a powerful, easy-to-use JavaScript unit testing framework. It's used by the jQuery, jQuery UI and jQuery Mobile projects and is capable of testing any generic JavaScript code

```js
QUnit.module("Group A");

QUnit.test( "deepEqual test", function( assert ) {
  var obj = { foo: "bar" };

  assert.deepEqual( obj, { foo: "bar" }, "Two objects can be the same in value" );
});

QUnit.module('Group B');

QUnit.test( "hello test", function( assert ) {
  assert.ok( "hello world" === "hello world", "Test hello wordl" );
});

```

>吐槽：

>1.如果你的app基于JQuery，建议你用此框架

>2.easy to set up, just a js and a css file

>3.每次开头都要打QUnit.module 或者 QUnit.test(烦不烦)

>4.module的分组方式不科学 （没有嵌套）

>5.语法最啰嗦

- 2.[Mocha](https://mochajs.org/)


>Mocha is a feature-rich JavaScript test framework running on Node.js and the browser, making asynchronous testing simple and fun. Mocha tests run serially, allowing for flexible and accurate reporting, while mapping uncaught exceptions to the correct test cases.

```js
//Synchronous
describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      [1,2,3].indexOf(5).should.equal(-1);
      [1,2,3].indexOf(0).should.equal(-1);
    });
  });
});

//Asynchronous Code
describe('User', function() {
  describe('#save()', function() {
    it('should save without error', function(done) {
      var user = new User('Luna');
      user.save(function(err) {
        if (err) throw err;
        done();
      });
    });
  });
});
```
>吐槽：

>1.对异步的支持，对promise的支持性不错

> 2.没有自带的Assertions 

> 		(1)should.js BDD style

> 		(2)chai expect(), assert() and should style assertions

>3.支持BDD语法 和 TDD语法

>		BDD：describe(), it(), before(), after(), beforeEach(), and afterEach()  

>		TDD：suite(), test(), setup(), and teardown()

> Reporters :[是最大的亮点](https://mochajs.org/)

- 3.[Jasmine](http://jasmine.github.io/)


>Jasmine is a behavior-driven development framework for testing JavaScript code. It does not depend on any other JavaScript frameworks. It does not require a DOM. And it has a clean, obvious syntax so that you can easily write tests. 


```js
describe("A suite", function() {
  it("contains spec with an expectation", function() {
    expect(true).toBe(true);
  });
});
```
>吐槽：

>版本1.x 和 2.x api有不少的变化 （runs，waitsFor在2.x不见了）

> 2.x版本开始对异步支持

> 对promise的支持性不够好 （1.x用jasmine-as-promise插件 2.x用jasmine-promise-matchers插件）

> 亮点： spy 还有 jasmine clock


#### Jasmine 自动化测试3种方式
- 浏览器直接打开
- 用karma ＋ gulp/grunt
- webStorm 自带的build in

#### what is TDD and How to TDD

>1.先写测试让其fail

>2.用最简单的方式让其pass

>3.分析用户情景／场景让其fail again，改进代码让其pass again

>4.对数据结构抽象，对性能进行优化等


#### 添加自动化测试的好处和注意事项

- 省去大量的，重复性的功能测试和回归测试
- 阅读测试description就像读英文一样，它是很好的情景分析工具，是开发手册。（e2e测试description就是一本用户手册）
- 省去项目越来越大，越来越乱，埋坑越来越多的问题。 重构？ 重写？
- 找bug方便，用test coverage和条件分支测试来除去冗余的代码
- 如果发现某代码非常难于测试，证明代码本来就有问题（dependency 很难mock，代码耦合度高）（例子：调用window对象太多，过多调用$parent或者$rootScope，在angular controler or linkFn 调用JQuery）
- 因为写代码的每时每刻都在refactor，TDD让你always focus on 用户的acceptance criteria(验收准则),不会多不会少，像一个圈圈在保护你的代码
 

#### Copyright

Copyright (c) 2015 [广发证券IT](http://it.gf.com.cn)



