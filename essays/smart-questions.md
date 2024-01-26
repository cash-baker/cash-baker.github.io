---
layout: essay
type: essay
title: "Smart Questions, Good Answers"
# All dates must be YYYY-MM-DD format!
date: 2024-01-25
published: false
labels:
  - Questions
  - Answers
  - StackOverflow
---

<img width="300px" class="rounded float-start pe-4" src="../img/smart-questions/rtfm.png">

## Is there such thing as a stupid question?

At some point, every programmer has been in a position where they felt like they hit a brick wall in their code. They tried googling solutions but are left with more questions than answers. There's no shame in asking for help and asking questions yourself. Asking questions fosters a healthly learning environment and should always be encouraged. But as we'll see, the quality of a question greatly affects the quality of the answers you recieve.   

## What’s a smart question?

A "smart question" should adequately provide a snapshot of the problem you've encountered. [Let's take this question for example.](https://stackoverflow.com/questions/32370994/how-to-pass-props-to-this-props-children)

```
I'm trying to find the proper way to define some components which could be used in a generic way:

<Parent>
  <Child value="1">
  <Child value="2">
</Parent>

There is a logic going on for rendering between parent and children components of course, you can imagine <select> and <option> as an example of this logic.

This is a dummy implementation for the purpose of the question:

var Parent = React.createClass({
  doSomething: function(value) {
  },
  render: function() {
    return (<div>{this.props.children}</div>);
  }
});

var Child = React.createClass({
  onClick: function() {
    this.props.doSomething(this.props.value); // doSomething is undefined
  },
  render: function() {
    return (<div onClick={this.onClick}></div>);
  }
});

The question is whenever you use {this.props.children} to define a wrapper component, how do you pass down some property to all its children?

```

The question 

```
A: datetime and the datetime.timedelta classes are your friend.

1. find today
2. use that to find the first day of this month.
3. use timedelta to backup a single day, to the last day of the previous month.
4. print the YYYYMM string you're looking for.

Like this:

 >>> import datetime
 >>> today = datetime.date.today()
 >>> first = datetime.date(day=1, month=today.month, year=today.year)
 >>> lastMonth = first - datetime.timedelta(days=1)
 >>> print lastMonth.strftime("%Y%m")
 201202
 >>>

```
 
The asker received six possible answers, and he or she was successful in inciting discussion from multiple users. The answers themselves were clear and were devoid of the rumored sarcasm and hostility of “hackers.” Since I myself have referenced this page and found it useful, I can confidently say that it is a good question.

## ..and not smart

Sometimes in life, we need to stop to ask ourselves.. [will eclipse no run classes?](https://stackoverflow.com/questions/77883350/will-eclipse-no-run-classes)

```
Q: Will eclipse no run classes? (-1 rating) 

I try to run my class and it says the selection cannot be launched, and there are no recent launches.

I tried to run it and I expected it to run but it just pops up with "the selection cannot be launched, and there are no recent launches."
```

There's a lot to unpack here. To start, the post title isn't grammatically sound and worded confusingly. They start by asking if Eclipse can launch classes but they're not looking for a simple yes or no answer, they're really asking why their class isn't launching which isn't communicated in the title. The biggest issue with this post is that it's too broad. The user is wondering why they can't launch their class in Eclipse, but includes no code snippets of the class or any other relevant code The only context we get is a quote of the error message. Ths question severely lacks any precise information needed to even solve their problem. The one response that the user recieved simply states that they need to show their code, and to add insult to injury refers them to StackOverflow's "How to Ask Questions" page. 

