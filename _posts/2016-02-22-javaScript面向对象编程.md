---
published: true
layout: post
title: javaScript面向对象编程
category: javaScript
tags: 
  - javaScript
time: 2016.02.22 17:19:00
excerpt: JavaScript的所有数据都可以看成对象，那是不是我们已经在使用面向对象编程了呢？当然不是。如果我们只使用Number、Array、string以及基本的{...}定义的对象，还无法发挥出面向对象编程的威力。

---

 <p>JavaScript的所有数据都可以看成对象，那是不是我们已经在使用面向对象编程了呢？</p>
<p>当然不是。如果我们只使用<code>Number</code>、<code>Array</code>、<code>string</code>以及基本的<code>{...}</code>定义的对象，还无法发挥出面向对象编程的威力。</p>
<p>JavaScript的面向对象编程和大多数其他语言如Java、C#的面向对象编程都不太一样。如果你熟悉Java或C#，很好，你一定明白面向对象的两个基本概念：</p>
<ol>
<li><p>类：类是对象的类型模板，例如，定义<code>Student</code>类来表示学生，类本身是一种类型，<code>Student</code>表示学生类型，但不表示任何具体的某个学生；</p>
</li>
<li><p>实例：实例是根据类创建的对象，例如，根据<code>Student</code>类可以创建出<code>xiaoming</code>、<code>xiaohong</code>、<code>xiaojun</code>等多个实例，每个实例表示一个具体的学生，他们全都属于<code>Student</code>类型。</p>
</li>
</ol>
<p>所以，类和实例是大多数面向对象编程语言的基本概念。</p>
<p>不过，在JavaScript中，这个概念需要改一改。JavaScript不区分类和实例的概念，而是通过原型（prototype）来实现面向对象编程。</p>
<p>原型是指当我们想要创建<code>xiaoming</code>这个具体的学生时，我们并没有一个<code>Student</code>类型可用。那怎么办？恰好有这么一个现成的对象：</p>
<pre><code>var robot = {
    name: &#39;Robot&#39;,
    height: 1.6,
    run: function () {
        console.log(this.name + &#39; is running...&#39;);
    }
};
</code></pre><p>我们看这个<code>robot</code>对象有名字，有身高，还会跑，有点像小明，干脆就根据它来“创建”小明得了！</p>
<p>于是我们把它改名为<code>Student</code>，然后创建出<code>xiaoming</code>：</p>
<pre><code>var Student = {
    name: &#39;Robot&#39;,
    height: 1.2,
    run: function () {
        console.log(this.name + &#39; is running...&#39;);
    }
};

var xiaoming = {
    name: &#39;小明&#39;
};

xiaoming.__proto__ = Student;
</code></pre><p>注意最后一行代码把<code>xiaoming</code>的原型指向了对象<code>Student</code>，看上去<code>xiaoming</code>仿佛是从<code>Student</code>继承下来的：</p>
<pre><code>xiaoming.name; // &#39;小明&#39;
xiaoming.run(); // 小明 is running...
</code></pre><p><code>xiaoming</code>有自己的<code>name</code>属性，但并没有定义<code>run()</code>方法。不过，由于小明是从<code>Student</code>继承而来，只要<code>Student</code>有<code>run()</code>方法，<code>xiaoming</code>也可以调用：</p>
<p><img src="/files/attachments/001435287613668a73ab76ccc85411282c1b1370be41636000/l" alt="xiaoming-prototype"></p>
<p>JavaScript的原型链和Java的Class区别就在，它没有“Class”的概念，所有对象都是实例，所谓继承关系不过是把一个对象的原型指向另一个对象而已。</p>
<p>如果你把<code>xiaoming</code>的原型指向其他对象：</p>
<pre><code>var Bird = {
    fly: function () {
        console.log(this.name + &#39; is flying...&#39;);
    }
};

xiaoming.__proto__ = Bird;
</code></pre><p>现在<code>xiaoming</code>已经无法<code>run()</code>了，他已经变成了一只鸟：</p>
<pre><code>xiaoming.fly(); // 小明 is flying...
</code></pre><p>在JavaScrip代码运行时期，你可以把<code>xiaoming</code>从<code>Student</code>变成<code>Bird</code>，或者变成任何对象。</p>
<p><em>请注意</em>，上述代码仅用于演示目的。在编写JavaScript代码时，不要直接用<code>obj.__proto__</code>去改变一个对象的原型，并且，低版本的IE也无法使用<code>__proto__</code>。<code>Object.create()</code>方法可以传入一个原型对象，并创建一个基于该原型的新对象，但是新对象什么属性都没有，因此，我们可以编写一个函数来创建<code>xiaoming</code>：</p>
<pre><code>// 原型对象:
var Student = {
    name: &#39;Robot&#39;,
    height: 1.2,
    run: function () {
        console.log(this.name + &#39; is running...&#39;);
    }
};

function createStudent(name) {
    // 基于Student原型创建一个新对象:
    var s = Object.create(Student);
    // 初始化新对象:
    s.name = name;
    return s;
}

var xiaoming = createStudent(&#39;小明&#39;);
xiaoming.run(); // 小明 is running...
xiaoming.__proto__ === Student; // true
</code></pre><p>这是创建原型继承的一种方法，JavaScript还有其他方法来创建对象，我们在后面会一一讲到。</p>

    </div>