### Slide 1 
Before the advent of HTML5, we had limited control over browser
history we were not able to control and manipulate the session
history of a particular browsing context. We could go back and forth
using the available methods, but that was not without incurring page
reloads or relying on <code>location.hash</code> workarounds. With
the HTML5 History API, we have more control with the browser
history. For example, we have a way to add an entry in the history,
or change the URL in the address bar without refreshing the page.

### Slide 2
Browser Support
Link to https://caniuse.com/#feat=history where we can check support of any feature by modern browsers. Here specifically History API.

### Slide 3
(Image 1) Picture where support of History API is shown. 

### Slide 4
If you like building apps without heavy frameworks or routing
libraries, this one's for you.
It allows us to build applications in an SEO-friendly manner.
Furthermore, this technique allows us to reduce bandwidth. That
means we will load all required resources on the first page load.
From there onward, the application will download only the required
contents. In other words, instead of loading all resources all the
time, it will load only required resources from a second content
request. Note that you need to perform some server-side coding to
deliver only partial resources instead of full page content.

### Slide 5
Another reason to use this API is because users love the browser's
back button.
It even won an award as the most pressed button in Firefox back in the day. So your app should definitely 100% expect that users will try to use the back button everywhere in your app to return to previous views.


### Slide 6
The History API relies on a single DOM interface the History object. There is a unique History object defined for each tab, accessed through the history attribute of the Window interface. This can be manipulated using JavaScript along with some special methods. To relate this to the actual pages in your session history, each Document object is associated
with a unique instance of the tab's History object (they all model the same underlying session history).

### Slide 7
History objects represent each tab's session history as a flat, comma-separated list of session history entries. Each session history entry consists of a URL or a state object (or both), and in addition can have a title, a Document object, form data, a scroll position, and other information associated with it.

### Slide 8
*`window.history.length`: Returns the number of entries in the joint session history.

*`window.history.state`: Returns the current state object.

*`window.history.go(n)`: Goes backwards or forwards by the specified number of steps in the joint session history. If the value you specify is zero, it will reload the current page. If it would cause the target position to be outside the available range of the session history, then nothing happens.

*`window.history.back()`: Goes backwards by one step in the joint session history. If there is no previous page to go to, it does nothing.

*`window.history.forward()`: Goes forwards by one step in the joint session history. If there is no next page to go to, it does nothing.

*`window.history.pushState(data, title [, url])`: Pushes the data specified in the arguments onto the session history, with the given title and URL (the URL is optional).

*`window.history.replaceState(data, title [, url])`: Updates the current entry in the session history, with the given data, title and URL (the URL is optional).

### Slide 9
The History API assumes that your view is a function of state that is, what is displayed on screen depends on a global state object. This allows the browser to store all your states so that when a user presses the back button, they return to the previous state as expected.
So to use the History API, you must have a global state of some kind that your views depend on.

### Slide 10
The flow looks like this: user event -> update state -> re-render
Every action should trigger a state change, which triggers a re-render.

### Slide 11
To use the browser's history functionality, you begin by telling the browser to remember your initial state. This requires the replaceState method like so: window.history.replaceState(state, null, ""). If you want to change URL be sure to update your server side code to handle the path.

### Slide 12
Whenever the user does something that updates state, such as clicking a checkbox or navigating to a different view, you will need to update your state and then store it in the browser. After updating your state, call this: window.history.pushState(state, null, ""). With every push, the browser gathers more and more states that it can cycle through if the user wants to start cycling back.

### Slide 13
The browser's back button triggers the onpopstate listener, which connects to the History API

```javascript
window.onpopstate = function (event) {
if (event.state) {
state = event.state;
}
render(state);
};
```

Event has a property state that has old state. Just set your application state to this old state and trigger a re-render to display the old state

### Slide 14
(Video 1) Here you can see how user can use it. When user clicks button a new object will be pushed into history stack and length of available states will be increased. When user will press Back button event will be poped and we will get apropriate state object. Then we can rerender interface with this data.

### Slide 15
Now we have some understanding of the History interface. We used pushState to add entries to the browsing context's history and the popstate event to react to state changes. What's more, each file that has been navigated to can be accessed later at its real URL. This highlights the real usefulness of the history API: you can create Ajaxy navigation in the style of Facebook or Twitter, without breaking the back button or the URLs to individual pages. Although bear in mind that hashbangs don't work if you share the URL with someone who has scripting disabled.