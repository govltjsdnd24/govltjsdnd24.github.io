---
categories: [ Development, React]
tags: [ react ] 
---

I've always been interested in studying React. It's not that I was incapable of developing the Front-end, but rather, I was: one, a Full-stack developer who was inclined towards Back-end, and two, even when I was working on the Front-end, I typically used Vue. While Vue is an excellent Front-end framework itself, it has relatively fewer templates and tools than React; overall, it is a less popular framework than React. Of course, the reason why I was <i>forced</i> to learn Vue in the first place was because it was just a simpler language due to the reduced amount of JavaScript's intervention in the code, but the sheer vast environment that React promised was just too enticing to ignore it. Hence is the reason why I volunteered to participate in the Front-end of our upcoming project.

## React Setup 
There is a very simple React tutorial available in their official documentation. Easy to follow and implement, I decided that this would be the perfect starting point. I will focus on the important parts in order to prevent my post from becoming just a replica of React tutorial.

Firstly, let's set up some things in order to make React work in our local environment. Download Node.js and Visual Studio Code, install React and Babel from Visual Studio Marketplace, and run the below code in the terminal to set up your first-ever React project. Note that npx (Node Package eXecute) is a supplementary tool for npm that adds some new features to the package manager.
```bash
npx create-react-app {{your-app-name}}
```
If you get an ugly error as such:

It's just that your create-react-app is not installed properly. Just reinstall it and it should work fine.


Also, note that if you are using a code editor such as Visual Studio Code, you can't run it by pressing the <i>Run</i> button, but have to rather use the terminal. "npm start" can be used to run the project.

When you see a big spinning React logo upon using the start command, congratulations, you've run a React project. 

## Tutorial
Now, we move on to the details of this framework. First thing one must note is JSX, which stands for Javascript Syntax eXtension. Since a large percentage of React project has to utilize Javascript, JSX is essential for the comprehension and abbreviation of the code. JSX code looks something like this:

A variable can now look like an HTML code block!


In React, each component can be expressed as a class extending React.Component, wherein there can be various methods; the render() method is the most quntessential method in the class component, responsible for the visual representation of the elements. There can be other methods such as constructor or handleClick, but if the class has render() as the singular method, it can be expressed as a function.

In order for components to communicate with each other, <i> props</i> or <i> state</i> can be used. Props are "propagated" to child components, and can be specified upon summoning of the child component.

Each component can also sustain a state by using a constructor method within the class. You must know that the props as parameter in constructor is not necessitated, but is recommended because there are many cases you want to use props in the constructor. Anyway, state is defined within the constructor as below

and accessed/used like below.

## Routing

That's about it for the tutorial, but we didn't cover routing yet did we? I created a fresh Vue project for this, and divided each component/element in an orderly fashion.


All the routers have to be located with in Routers, and when laid out it looks something like this.

There were some troubleshooting involved in this part because I was referring to a somewhat dated material. The tag `<Route>` has to be used instead of `<Switch>` because the latter is deprecated.

Also, each component is recommended to be referred to as element rather than component because, after v6 update of React, the rendering process of a component has been simplified to work with an arrow function as long as you use 'element'.

So, after all the routing and what-not, I was able to successfully run a local server (I used a template available online for the navigation bar.)


## Conclusion 
I wanted to keep it short but seems like it is impossible for me to do that. I mean, I had to include all the vital points I stumbled upon, and everything seems vital...! Anyway, this was my futile attempt to come up with a brief demonstration of React implementation, and I'll update my React website along with it.

## Reference
[https://legacy.reactjs.org/tutorial/tutorial.html](https://legacy.reactjs.org/tutorial/tutorial.html)
[https://goddaehee.tistory.com/305](https://goddaehee.tistory.com/305)




