# 3-1-3-lab-ticket-markdown
Copy and paste each section to a separate ticket on you scrum board for you lab. If you have any questions reach out to your instructor or TA.
<hr>

Section 1.1 - getFirstThreeFantasyBooks

Inside fetch-functions.js you need to write a function getFirstThreeFantasyBooks. This function takes in no arguments, and returns 3 books of the fantasy genre. Here's the URL you should work with:

https://openlibrary.org/subjects/fantasy.json

**Function requirements**

- [ ] It should send a fetch request to the correct URL (this is not a trick question, make sure to use the URL listed above)
- [ ] It should return a promise
- [ ] If there are no errors, the returned promise should resolve to an array of the first 3 books from the API
- [ ] Format each book in the array to look like this: 

> 
```js
[
  {
    title: "Alice's Adventures in Wonderland",
    author: {
      name: "Lewis Carroll",
      urlKey: "/authors/OL22098A",
    },
    coverUrl: "https://covers.openlibrary.org/a/id/10527843-M.jpg"
  },
  // 2 more items
]
```
For more information, check the data formatting section!

- [ ] If there is a fetch error, catch the error,. console.warn the error message, and the returned promise should resolve to null.
- [ ] If API response is not ok, then you should throw an error with a message of "Failed to get fantasy books"
- [ ] If you set up your function right, that means your function would console.warn the error message, and then resolve to null
- [ ] We do mean "first 3" — we double checked that URL, and there are definitely 3 books that meet all our needs. Please maintain the order so the tests pass (no sorting the books or anything)

<hr>

Section 1.1 - test: Data-collection

You can certainly test out your progress by running `npm test`, however you should also test out your code by invoking your function.

In app.js, you can see that we've imported your getFirstThreeFantasyBooks function. As you see in app.js there's already a decent amount of code written out. Do not remove any existing code (or change things like IDs) as the tests need these to run.

Towards the bottom of the app function, look for the `// Fetch the books!` comment. There you can invoke getFirstThreeFantasyBooks() and console.log the returned set of books.

Run the program with npm run dev and pop open your console to view your logs. If you see your array of 3 books, you should be good to go!

Alright, with that, you should be all set to move on!

<hr>

Section 1.2 - renderBooksToDOM

### Description: 
Now that we have our data, we need to render it to the screen. You need to write a function `renderBookList` in **render-functions.js**, that takes in a `bookListEl` (a ul HTMLElement) and an array of books. These are the books our fetcher function will return! This function will mutate the passed in `bookListEl` and add a bunch of li elements to it, one for each book.

### Goal: 
- The goal is to display elements on the DOM using our fetcher function! Do not worry about adding functionality to our elements just yet! That will be in a separate ticket. 

### Function Requirements:

- [ ] The function should remove any existing children from the passed in `bookListEl`

- [ ] It should add a series of li elements to the `bookListEl` for each book in the books array

- [ ] Each `li` should have (in this order)
  - [ ] an `img` tag with a `src` of the `coverUrl` and an `alt` of An old cover of [BOOK TITLE]
  - [ ] a `p` tag with the text Title: [BOOK TITLE]
  - [ ] a `button` tag with the text View [AUTHOR NAME]
  - [ ] `data-author-url-key` attribute with the value of `author.urlKey`


### Example:

<li>
  <img src="https://covers.openlibrary.org/a/id/13859660-M.jpg" alt="An old cover of Treasure Island">
  <p>Title: Treasure Island</p>
  <button data-author-url-key="/author/OL25963A">View Robert Louis Stevenson</button>
</li>

### Example HTML:

```html
<li>
  <img src="https://covers.openlibrary.org/a/id/13859660-M.jpg" alt="An old cover of Treasure Island">
  <p>Title: Treasure Island</p>
  <button data-author-url-key="/author/OL25963A">View Robert Louis Stevenson</button>
</li>
```

<hr>

Section 1.2 - test: Rendering-books

### Testing
What you need to do here is use your fetch function `getFirstThreeFantasyBooks` to get some books, and then invoke `renderBookList` with the already created `bookListEl` variable and your fetched books to render your books to the screen!

You'll know you've done it if the tests are passing and the page loads up your books!

### Slow API
While your playing around, you may worry that your images won't load. That's fine, this is not exactly the fastest api in the world. It takes a bit for the images to load up. If they eventually show up (and if your tests are passing), you're all set! (This is a prime example of why you mock things in tests)

### Data Layer separation
Do not call your fetching functions in your render functions! We want to keep our data layer and presentation layer separate.

<hr>

Section 2.1 - getAuthor

### Description
Inside `fetch-functions.js` we need to create the `getAuthor` function. It will take in a urlKey that we got from getThreeFantasyBooks. That means this time we can't hardcode the url. Look at the url we want to hit:

https://openlibrary.org/authors/{SOME_ID}.json

Just like before, we'll need to do some formatting of the data as well.

### Function Requirements

- [ ] It should make a fetch to the correct, dynamic url

- [ ] It should return a promise

- [ ] If there are no errors, it should resolve a formatted author object (see Data Formatting below for more details)

- [ ] If there is a fetch error it should resolve null and console.warn the error message

- [ ] If the API response is not ok, then you should throw an error with a message of Failed to get author

- [ ] If you set up your function right, that means your function would console.warn the error message, and then return null

### Data formatting

```js
{
  birthDate: 'January 27, 1832',
  bio: 'Lewis Carroll is well known throughout the world as BLAH BLAAAHHHH BLAAAHHH MORE STUFF',
  wikipediaLink: 'http://en.wikipedia.org/wiki/Lewis_Carroll',
  name: 'Lewis Carroll',
  pictureUrl: 'https://covers.openlibrary.org/a/id/6285807-M.jpg',
}
```

<hr>

Section 2.2 - renderAuthor

### Description: 
Go into `render-functions.js` and write a function named `renderAuthor` that takes in a `div` element and an author object and renders it to the screen. This function will mutate the passed in div element. Here are the specific tags to add (in order and ONLY add these tags)

### Function Requirements

- [ ] An h2 with the text [AUTHOR NAME]

- [ ] An `img` tag with a `src` of the picture and an `alt` of A picture of [AUTHOR NAME]

- [ ] A `p` tag with the text Born: [AUTHOR BIRTH DATE]

- [ ] A `p` tag with the text from the bio property

- [ ] An a tag with an href of the `wikipediaUrl` property and the text Wikipedia Link

- [ ] `renderAuthor` should clear out the passed in div of any existing children before adding these new ones. 

### Extra Information: 
 > We're going to render every author to the same div to keep things simple and we don't want them to accumulate.

<hr>

Section 2.3 - addEventListenerForAuthors

### Description: 

We need to make sure that we are rendering author data based on the button that was clicked but we do not have that functionality just yet! Here is how you can implement that logic! Each book in the books list has a button with a dataset attribute of the required author key so let's use that!

### Function Requirements: 

- [ ] Attach a `click` listener to the list element with all our books, 
- [ ] Handle the click event so that any time a button is clicked, we get the author data with `getAuthor` 
- [ ] After we handle the click event, render it to the author-info div.

### Additional Information:

This action only has to fire when the user clicks the button, you don't need to load a default author or anything like that. Just make sure you're getting the right author for the right book!

<hr>

Section 3.1 - createNewUser

### Description: 
Finish the last function in `fetch-functions.js` called `createNewUser`. This will need to take in a user object as the only argument. 

### Function Requirements: 

- [ ] Create a new user

- [ ] If the request is successful, return the new user object that you get back

- [ ] Don't just hardcode 11 in your function.

- [ ] If there is an error with the fetch, you should return null and console.warn the error message

- [ ] If the response is not ok then you should throw an error with the message: `Failed to create new user`

### Data Format:

```js
{
  username: 'Zo_Bro',
  isCool: true,
  favoriteLanguage: 'JavaScript',
}
```
### Additional Information: 

> https://jsonplaceholder.typicode.com/ is the host
JSON placeholder follows RESTful conventions
Example of RESTful Conventions: 
GET -> /pets
POST -> /pets 
PATCH/PUT -> /pets/:id
DELETE -> /pets/:id

<hr>

Section 3.2 - renderNewUserForm

### Description: 

Unlike the other sections, we need some way for a user to enter information. We will create a function that will take in a form element and edit the form to render some HTML.  You will need to mutate the form!

### Function Requirements: 

- [ ] Create a function `renderNewUserForm` in `render-functions.js` that takes in a form element.

- [ ] A `label` with the text Username

- [ ] An `input` with an `id` of username and a `name` of username

- [ ] A `label` with the text: Is this user cool?

- [ ] An `input` with an `id` of `is-cool`,  a `name` of `isCool` and a `type` of checkbox

- [ ] A `label` with the text: Favorite Language

- [ ] A `select` with an `id` of `favorite-language` and a `name` of `favoriteLanguage` and the following options in this order. The list below is both the text and the value of the option:

  - [ ] None
  - [ ] JavaScript
  - [ ] Python
  - [ ] Ruby

- [ ] A button with the text Create User to submit the form.

### Additional Information: 
> Do not attach any events here, just render the HTML. We'll attach the events later. 
The tests are exact!

<hr>

Section 3.3 - renderNewUser

### Description: 

Unlike the other sections, we need some way for a user to enter information. We will create a function that will take in a form element and edit the form to render some HTML.  You will need to mutate the form!

### Function Requirements: 

- [ ] Create a function `renderNewUserForm` in `render-functions.js` that takes in a form element.

- [ ] A `label` with the text Username

- [ ] An `input` with an `id` of username and a `name` of username

- [ ] A `label` with the text: Is this user cool?

- [ ] An `input` with an `id` of `is-cool`,  a `name` of `isCool` and a `type` of checkbox

- [ ] A `label` with the text: Favorite Language

- [ ] A `select` with an `id` of `favorite-language` and a `name` of `favoriteLanguage` and the following options in this order. The list below is both the text and the value of the option:

  - [ ] None
  - [ ] JavaScript
  - [ ] Python
  - [ ] Ruby

- [ ] A button with the text Create User to submit the form.

### Additional Information: 
> Do not attach any events here, just render the HTML. We'll attach the events later. 
The tests are exact!

<hr>

Section 3.3 - renderNewUser

### Description: 
The goal for this ticket is to render a new user to the screen. You will create a function that takes in a div and user and renders HTML. 

### Function requirements: 

- [ ] Create a function `renderNewUser` in `render-functions.js` that takes in a `div` element and a user object 

- [ ] `h2` with the text of the `username` property

- [ ] `h2` must also have a `dataset` attribute of `userId` with the value of the `id` property

- [ ] `p` tag with the text: 
  - [ ] if the `isCool` property is `true`: "The hippest in the house!" 
  - [ ] if the `isCool` property is `false`: "A real square."

- [ ] `p` tag with the text: "Favorite Language: [FAVORITE LANGUAGE]"

- [ ] Remove any child elements from the passed in `div` element to avoid repeating any tags.


<hr>

Section 3.4 - addEventListenerForUsers

Description: 
We need to be able to dynamically add users so that when a user submits a form, we render their specific information!

### Function Requirements: 

- [ ] Render the form
- [ ] Attach an event listener to the form to handle submits
- [ ] The submission handler should call `createNewUser` with the form data (careful with that checkbox value! It's not a boolean by default...)
- [ ] After creating the user, call `renderNewUser` with the `newUserDiv` and the new user object
