
# A Flavor of Directives.



In this chapter we are going through some basic examples of Vue's directives.
Well,
if you have not used any Framework like Vue.js or AngularJS before, you probably don't know what a directive is.
Essentially, a directive is some special token in the markup that tells the library to do something to a DOM element.
In Vue.js, the concept of directive is drastically simpler than that in Angular.
Some of the directives are:  

* **`v-show`** which is used to conditionally display an element
* **`v-if`** which can be used instead of **`v-show`**
* **`v-else`** which displays an element when **`v-if`** or **`v-show`** evaluates to false.

Also, there is **`v-for`**, which requires a special syntax and its use is for rendering
(e.g. render a list of items based on an array).
We will elaborate about the use of each later in this book.



Let us begin and take a look at the directives we mentioned.



## v-show



To demonstrate the first directive we are going to build something simple.
We will give you some tips that will make your understanding and work much easier!
Suppose you find yourself  in need to toggle the display of an element, based upon some set of criteria.
Maybe a submit button shouldn't display unless you've first typed in a message.
How can we accomplish that with Vue?



{lang="HTML"}
    <html>
    <head>
        <title>Hello Vue</title>
    </head>
    <body>
    <div id="app">
        <textarea></textarea>
    </div>
    </body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                 message: 'Our king is dead!'
            }
        })
    </script>
    </html>



Here we have an HTML file with our known **`div id="app"`** and a **`textarea`**.
Inside the **`textarea`** we are going to display our message.
Of course, it is not yet binded and by this point you may have already figured it out.
Also you may have noticed that in this example we are no longer using the minified version of Vue.js.
As we have mentioned before, the minified version shouldn't be used during development because you will miss out warnings for common mistakes.
From now on we are going to use this version in the book but of course you are free to do as you like.



{lang="HTML"}
    <html>
    <head>
        <title>Hello Vue</title>
    </head>
    <body>
    <div id="app">
        <textarea v-model="message"></textarea>
        <pre>
            {{$data | json}}
        </pre>
    </div>
    </body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                 message: 'Our king is dead!'
            }
        })
    </script>
    </html>




It is time to bind the value of **`textarea`** with our **`message`** variable using **`v-model`** so it displays our message.
Anything we type in is going to change in real time, just as we saw in the example from the previous chapter,
where we were using an input.
Additionally, here we are using a **`pre`** tag to spit out the data.
What this is going to do, is to take the data from our Vue instance,
filter it through **`json`**, and finally display the data in our browser.
We believe, that this gives a much better way to build and manipulate our data,
since having everything right in front of you is better than looking constantly at your console.


I> ## Info
I>
I> JSON (JavaScript Object Notation) is a lightweight data-interchange format.
I> You can find more info on JSON [here](http://www.json.org/).
I> The output of  **`{{$data | json}}`** is binded with Vue data and will get updated on every change.



{lang="HTML"}
    <html>
    <head>
        <title>Hello Vue</title>
    </head>
    <body>
    <div id="app">
        <h1>You must send a message for help!</h1>
        <textarea v-model="message"></textarea>
        <button v-show="message">
            Send word to allies for help!
        </button>
        <pre>
            {{$data | json}}
        </pre>
    </div>
    </body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                 message: 'Our king is dead! Send help!'
            }
        })
    </script>
    </html>




Carrying on, we now have a simple warning in the **`h1`** tag that will toggle later based on some criteria.
Next to it, there is the button which is going to display conditionally. Ιt appears only if there is a message present.
If the **`textarea`** is empty and therefore our data, the button's **`display`** attribute is automatically
set to 'none' and the button disappears.



I> ## Info
I>
I> An element with **`v-show`** will always be rendered and remain in the DOM. **`v-show`** simply toggles the **`display`**
I> CSS property of the element.




{lang="HTML"}
    <h1 v-show="!message">You must send a message for help!</h1>
    <textarea v-model="message"></textarea>
    <button v-show="message">
        Send word to allies for help!
    </button>





What we want to accomplish in this example, is to toggle different elements.
In this step, we need to hide the warning inside the **`h1`** tag, **if** a message is present. Οtherwise hide the message by setting its **`style`** to **`display: none`**.



## v-if



In this point you might ask 'What about the v-if directive we mentioned earlier?'.
So, at this point we will build the previous example again, only this time we'll  use **`v-if`**!



{lang="HTML"}
    <html>
    <head>
        <title>Hello Vue</title>
    </head>
    <body>
    <div id="app">
        <h1 v-if="!message">You must send a message for help!</h1>
        <textarea v-model="message"></textarea>
        <button v-show="message">
            Send word to allies for help!
        </button>
        <pre>
            {{$data | json}}
        </pre>
    </div>
    </body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                 message: 'Our king is dead! Send help!'
            }
        })
    </script>
    </html>




As shown, the replacement of **`v-show`** with **`v-if`** works just as good as we thought.
Go ahead and try to make your own experiments to see how this works!
The only difference is that an element with **`v-if`** will not remain in the DOM.



###Template v-if


If sometime we find ourselves in a position where we want to toggle the existence of
multiple elements at once, then we can use **`v-if`** on a **`<template>`** element.
In occasions where the use of **`div`** or **`span`** seems appropriate, the **`<template>`**
element can serve also as an invisible wrapper.
Also the **`<template>`** won 't be rendered in the final result.



{lang="HTML"}
    <div id="app">
        <template v-if="!message">
          <h1>You must send a message for help!</h1>
          <p>Dispatch a messenger immediately!</p>
          <p>To nearby kingdom of Hearts!</p>
        </template>
        <textarea v-model="message"></textarea>
        <button v-show="message">
            Send word to allies for help!
        </button>
        <pre>
            {{$data | json}}
        </pre>
    </div>




![Template v-if](images/screenshots/flavor/teif.png)


Using the setup from the previous example we have attached the **`v-if`** directive to the **`template`** element,
toggling the existence of all nested elements.



W> ## Warning
W>
W> The **`v-show`** directive does not support the **`<template>`** syntax.




## v-else



When using **`v-if`** or **`v-show`** you can use the **`v-else`**  directive to indicate an “else block”
as you might have already imagined.
Be aware that the **`v-else`** directive must follow immediately the **`v-if`** or **`v-show`**
directive - otherwise it will not be recognized.




Using  **`v-else`**  with  **`v-show`.**



{lang="HTML"}
    <html>
    <head>
        <title>Hello Vue</title>
    </head>
    <body>
    <div id="app">
        <h1 v-show="!message">You must send a message for help!</h1>
        <h2 v-else>You have sent a message!</h2>
        <textarea v-model="message"></textarea>
        <button v-show="message">
            Send word to allies for help!
        </button>
        <pre>
            {{$data | json}}
        </pre>
    </div>
    </body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                 message: 'Our king is dead! Send help!'
            }
        })
    </script>
    </html>





Using  **`v-else`**  with  **`v-if`.**



{lang="HTML"}
    <html>
    <head>
        <title>Hello Vue</title>
    </head>
    <body>
    <div id="app">
        <h1 v-if="!message">You must send a message for help!</h1>
        <h2 v-else>You have sent a message!</h2>
        <textarea v-model="message"></textarea>
        <button v-show="message">
            Send word to allies for help!
        </button>
        <pre>
            {{$data | json}}
        </pre>
    </div>
    </body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                 message: 'Our king is dead! Send help!'
            }
        })
    </script>
    </html>



![v-if in action](images/screenshots/flavor/viff.png)


![v-else in action](images/screenshots/flavor/vels.png)




Just for the sake of the example we have used an **`h2`** tag with a different warning
than before, which is displayed conditionally.
If no message is presented, we see the **`h1`** tag. 
If there is a message, we see the **`h2`** using this very simple syntax of Vue **`v-if`** and **`v-else`**.
As you can see above we've used **`v-if`** as well as **`v-show`**. Both give us the same result.
Simple as a pimple!





## v-if vs. v-show



Even though we have already mentioned a difference between **`v-if`** and **`v-show`** , we can deepen a bit more.
Some questions may arise out of their use.
Is there a big difference between using **`v-show`** and **`v-if`**?
Is there a situation where performance is affected?
Are there problems  where you're better off using one or the other?
You might experience that the use of **`v-show`** on a lot of situations causes bigger time of load during page rendering.
In comparison, **`v-if`** is truly conditional according to the guide of Vue.js.



> _When using **`v-if`**, if the condition is false on initial render,
it will not do anything - partial compilation won’t start until the condition becomes true for the first time.
Generally speaking, **`v-if`** has higher toggle costs while **`v-show`** has higher initial render costs.
So prefer **`v-show`** if you need to toggle something very often, and prefer **`v-if`** if the condition\ is unlikely to change at runtime._

So, when to use which really depends on your needs.

{icon=file-code-o}
G> ## Code Examples
G>
G> You can find the code examples of this chapter on [GitHub](https://github.com/hootlex/the-majesty-of-vuejs/tree/master/examples/3.%20A%20Flavor%20Of%20Directives).


{pagebreak}

## Homework

Following the previous homework exercise, you should try to expand it a bit.
The user now types in his gender along with his name.
If user is a male, then the heading will greet the user with **"Hello Mister {{name}}"**.
If user is a female, then **"Hello Miss {{name}}"** should appear instead.

When gender is neither male or female then the user should see the warning heading **"So you can't decide. Fine!"**.

{icon=lightbulb-o}
G> ## Hint
G>
G> A logical operator would come handy to determine user title.

![Example Output](images/screenshots/3.png)

{icon=sticky-note-o}
G> ## Note
G>
G> The example output makes use of Bootstrap.
G> If you are not familiar with bootstrap you can ignore it for now, it is covered in a [later chapter](#bootstrap).

You can find a potential solution to
this exercise [here](https://github.com/hootlex/the-majesty-of-vuejs/blob/master/homework/chapter3.html).
