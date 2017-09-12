# 🛠 Objects are tools, not a way of coding

Ta Daaaa…Controversy! I know, I know, blasphemy, burn him at the stake, and all that good stuff. But hear me out.

I started developing in 2000, when developers were transitioning from CGI to PHP, and PHP had no concept of objects. I transitioned to Java, then took a break from coding. When I came back full force in the world of NodeJS, I restarted to code in a functional way.

As time passed, I discovered that ES6 had full support for classes to create an objects. It turns out that “real” classes were introduced to help Java developers transition to JS. And I’m like, what? Why? 

Anyway, I continued with my functional coding (using object as key=vale arrays), but kept seeing classes and objects popping up more and more. Then I saw code done by Java developers in NodeJS and I go, damn. OK, creating a super complex object out of a class just to get the name of a user from the DB was really overkill. 

But I tagged along and did my functional thing. 

Then I saw that the developers' APIs were in the range of 400 ms to 1000 ms. And I began to wonder what was going on. I read some articles about companies that moved from Heroku to AWS because their APIs were slow. And my skepticism grew, since Heroku uses AWS…Sure, Heroku packs more accounts on one server, but still…Blaming it on the server didn’t seem right, especially when they went from 350 ms down to 250 ms to get some basic item information to display on a site. It seemed to me that the issue was with the code, rather than with the servers. 

# The Big Bang

Initially, object-oriented languages were geared toward modeling the real world, but their benefits also extended to the ability to easily cache data from the hard drive into memory thanks to its design. With functional programming, you have to purposely do this.

With a local setting - a computer, smartphone, or anything that is constantly running and has a user in front of it - OO is definitely the way to go. Easier, better, and all that good stuff. 

# But

Back in the day, universities started teaching Java as the main language. This made sense back then, since the web was, you know… a joke, nothing serious, and learning CGI or PHP and building sites were just hobbies. 

But as I’m writing this, we all know what the web turned out to be. 

I remember the debate over adding support for Objects into PHP. Two camps popped up: those who were excited about the prospect, and those who didn’t see the point. The main idea behind introducing Classes into PHP was to attract Java developers to PHP, and to help them make the transition. 

Side note: The word transition implies that you start doing it one way, and then you learn the right way. But we know how the human mind works; if it feels comfortable, we stick with it.

The same thing happened with JavaScript in version ES6 of the standard. JS already allowed you to build objects. Hell, you could make a full-fledged object in more ways than you have fingers on your left hand. But they introduced the concept of a Class, a structure to describe how to create an object, which is 1:1 how it's done in Java. The syntax is exactly the same, which I like, since it's very clean and simple to work with.

Why did they do this? Literally to help Java developers make the transition to JavaScript. And how do people code for the web today? With Classes, because of muscle memory, not because it make sense. 

# Let me explain: mobile app 

If you were creating a mobile app, you would have a User Class that would be loaded into memory when the app started, and the constructor would kick in code that would load some user data from SQLite, such as the Name, Last Name, and Avatar. Of course, the Class would have functions to return the name, last name, and avatar, along with reversing the text and inverting the image colors as a joke for Primas Aprilis. Heck, even functions to update the data.

This information would stay in memory, so you wouldn't stress the built-in storage every time you have to display this information, and it would be faster. This seems obvious and just makes sense.

# Let me explain: back-end server

Here, you do the exact same app, but instead of being on a mobile device it's done as an API written in NodeJS and connected to a nice database. Every time a user visits your site, you have an API called /me, which you query every time you want to show the user data (You can cache this in the browser it self, but that's not the point right now).

With back-end code, you can’t take advantage of the memory caching an object, since each request lives until the connection closes, and there is no state that you can take advantage of (There is, but again, not the point).

In this case, you are only left with the concept of representing data in a “natural” way. 

# And here's where I start to have an opinion

I believe that in the back-end world, the benefit of a Class is virtually zero. Once you start getting tens of thousands of requests per second, your code is just literally creating and destroying object at each request...For what? Because you are used to coding this way? Seems like a big waste of resources to me. 

By the way, did you realize the I've just been talking about the back end rather than the front end all this time? Bazinga! ;)

# Only functions in the back end

If you did the /me API in a functional way, when you received a request, you would just make a simple selection from the DB, return back the result as JSON, and that's it. This is the whole request. You don't need to create and then destroy anything. If you want to have some sort of transformation for Prima Aprilis, you can make an additional promise in the chain that will trigger on the right date or when you pass an argument in the URL. Done. The API will just fly.

# Do you use Classes at all?

Yes, when I’m dealing with a situation in which something or someone stays indefinitely connected to my back end. For example:

I had this project in which I was asked to wrap a modern RESTful API around an access control device that was designed more then 15 years prior, and the only way you could communicate with it was with a raw socket connection and a custom protocol. Once connected, the device stayed connected as long as the connection stayed up or the device had power. You could see that we had an active and persistent connection to the server. Here, I made a nice Class that mimicked the device connected to the server. In this case

When a device connects, the code creates an object out of my Class. I then query the device to ask for any additional data that's needed, and part of the data stays in memory.

On the other hand, the API part of the server is just functional. The API has access to all of the connected objects/devices, and I just query the object for the right data. For example:

Ask an API endpoint to give back the number of doors it controls, and the API uses a function of the Device Object to retrieve that number. 

If you have to open a door remotely with the API, another function would fire on that Device Object, and that request would then... 

- ...be translated inside the object in the special protocol
- ...send the request to the device
- ...wait for the response
- ...parse the response
- ...translate the response form that custom protocol in to JSON
- ...and send it back to whoever made the API request.

I believe this was one of those situations in which I was happy that JavaScript had Classes, because I was able to make a nice server that just works beautifully, and I’m proud of it. 

This situation is perfect Object Orientism 😊. I treat OO as just another tool that I have at my disposal to solve a specific problem in a specific way. And use functional programming to solve another problem with the right tool.

# So what do you think?

Do you still think OO is a way of coding, or is it just another tool in your tool box?

# The End

If you've enjoyed this article/project, please consider giving it a 🌟 or donate.

- [![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/gattidavid/25)
- [![Star on GitHub](https://img.shields.io/github/stars/davidgatti/Objects-are-tools-not-a-way-of-coding.svg?style=social)](https://github.com/davidgatti/How-to-Stream-Movies-using-NodeJS/stargazers)
- [![Watch on GitHub](https://img.shields.io/github/watchers/davidgatti/Objects-are-tools-not-a-way-of-coding.svg?style=social)](https://github.com/davidgatti/How-to-Stream-Movies-using-NodeJS/watchers)

Also check out my [GitHub account](https://github.com/davidgatti), where I have other articles and apps that you might find interesting.

## For Hire 👨‍💻

If you'd like me to help you, I'm available for hire. Contact me at job@gatti.pl.

## Where to follow

You can follow me on social media 🐙😇, at the following locations:

- [GitHub](https://github.com/davidgatti)
- [Twitter](https://twitter.com/dawidgatti)
- [Instagram](https://www.instagram.com/gattidavid/)

## More about me

I don’t only live on GitHub, I try to do many things not to get bored 🙃. To learn more about me, you can visit the following links:

- [Podcasts](http://david.gatti.pl/podcasts)
- [Articles](http://david.gatti.pl/articles)
- [Technical Articles](http://david.gatti.pl/technical_articles)
- [Software Projects](http://david.gatti.pl/software_projects)
- [Hardware Projects](http://david.gatti.pl/hardware_projects)
