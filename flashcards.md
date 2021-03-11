# Project: Flashcard-o-matic
Hi friends! I appreciate your time in reading this! This Flashcard website is a big project filled with big work. You are pretty much going to build up this entire app by yourself, but I've created this guide if you find yourself getting lost or looking for guidance. This project is really rewarding at the end - so don't let the bumps and frustrations you run into along the way deter you. You are capable. You can do it.

I designed this guide such that you can reference sections as you work along on the project, instead of reading it all at once.

1. **Starter Code**
	* Steps to fix `npm start` failing to run
1. **Getting Started**
	* Roughly skeleton out your components
1. **Bootstrap Components**
	* Breadcrumbs
	* Buttons
	* Cards
	* List Groups
1. **Icons** *(optional)*
	* Putting cute icons into your JSX
1. **Utility Functions**
	* Reference of all utility functions
	* Using a utility function: example
1. **Important Notes**
	* `deck.cards` array
	* `window.confirm()`
	* `useParams()` return type
	* `parseInt()`
	* Checking if Object is empty
1. **How to Pass Qualified Tests**
	* What you should aim for with each test.
---

## **1. Starter Code**

For some reason, the starter code that came from my Qualified did not work right out of the gate. (You'll know if your code won't work if `npm start` will not run.) If yours is like this too, here are the steps I took to fix the issue:

Note that I downloaded my code about a week before you did, so this problem very well might not exist anymore.

### `index.js` *(`src/Layout`)*
* Add the following import to the top of the file: 
`import React, { Fragment } from "react";`
* Change the `<></>` tags to `<Fragment></Fragment>` in the `return` statement.

### `package.json`
* Change the `start` script to the following: 
`"concurrently \"npm run start:server\" \"npm run start:react\"",`

Now, `npm start` should work.

---

## **2. Getting Started**
If you're someone who likes Bootstrap and designing the user interface of apps, you'll love the start of this project. You will be recreating the web pages shown in the instructions by creating React components and putting them together. It doesn't have to look the same, as long as the page you created has all functionality. You can decide how creative you would like to go for this project!

**My suggestion  is to start off with a rough plan of the components you plan to create.** By looking at each screenshot and jotting down some ideas of single-responsibility components, you cut down time later.

Here is a screenshot Thinkful gives us in the instructions:
![Example Screenshot](https://res.cloudinary.com/strive/image/upload/w_1000,h_1000,c_limit/f63b8bedaaf37cd8c3245febe6f0275f-deck.png)

As an example, I could decide to break up this screenshot into four different components:
1. Header, which is already made for you. *(`Header.js`)*
1. Breadcrumb
1. Deck Info
1. Card Info

After going through each screenshot, you already will have a rough skeleton of how to design and structure your app. You may end up changing or breaking down the components later, but hopefully you'll have a list of components we can work with and start developing!

---

## **3. Bootstrap Components**
Here are some Bootstrap components you may encounter when building your app. All code is written in JSX.

*Note: if you are to reuse code from Bootstrap's docs, you will have to change every `class` property to `className` to be compatible with React.*

### [Breadcrumbs](https://getbootstrap.com/docs/5.0/components/breadcrumb/)
```javascript
<nav aria-label="breadcrumb">
  <ol className="breadcrumb">
    <li className="breadcrumb-item"><a href="#">Home</a></li>
    <li className="breadcrumb-item"><a href="#">Link</a></li>
    <li className="breadcrumb-item active" aria-current="page">Current Page</li>
  </ol>
</nav>
```

### [Buttons](https://getbootstrap.com/docs/5.0/components/buttons/)
```javascript
<>
	<button type="button" className="btn btn-primary">Blue Button</button>
	<button type="button" className="btn btn-secondary">Grey Button</button>
	<button type="button" className="btn btn-warning">Red Button</button>
</>
```

### [Cards](https://getbootstrap.com/docs/5.0/components/card/)
```javascript
<div className="card">
  <div className="card-body">
    <h5 className="card-title">Card title</h5>
    <h6 className="card-subtitle mb-2 text-muted">Card subtitle</h6>
    <p className="card-text">Card text</p>
  </div>
</div>
```

### [List Groups](https://getbootstrap.com/docs/5.0/components/list-group/)
```javascript
<ul className="list-group">
  <li className="list-group-item">An item</li>
  <li className="list-group-item">A second item</li>
  <li className="list-group-item">A third item</li>
</ul>
```

---

## **4. Icons** *(optional)*
"What are those cute icons on the buttons?? I want to do that!" Fret no more. I will tell you how to integrate icons into your JSX!

[Bootstrap Icons](https://icons.getbootstrap.com/) is a place with free icons to integrate into your code. You will have to run `npm i bootstrap-icons` in your root project folder to use them.

### Example button with [Trash Can](https://icons.getbootstrap.com/icons/trash-fill/) icon:
```javascript
<button type="button" className="btn btn-danger">
	<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" className="bi bi-trash-fill" viewBox="0 0 20 20">
		<path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"/>
	</svg>
</button>
```
No - you don't have to know how to write that. Yeah - it's pretty awful to look at, but it makes your front end pretty at least. Search for icons you want to put into your app, and press "Copy HTML" and paste right into your code.

---

## **5. Utility Functions**
Import statement for reference: `import { ... } from "../utils/api/index.js"`, replacing the `...` with the function you wish to export.

These utility functions are mega fun! Sarcasm. Every utility function is an asynchronous function that returns JSON files wrapped in a Promise. It deals with all of the data found in `db.json`. You do not edit this file manually, instead, you use these functions to get/set data within the database.

*Please keep in mind:*
* *Every one of these functions need to be used at least once in your app.*
* *Every one of these function's returns are wrapped in a Promise.*
* *A `signal` parameter is an *optional* `AbortController.signal`.*

You can browse `index.js` in `utils/api` for all of the functions, but for ease of reference, I've put the functions below. 

> * `listDecks(signal)`
> 	* Returns an array of decks in the database.
> * `createDeck(deck, signal)`
> 	* `deck` must not have an `id` property (the function will make one automatically)
> 	* Returns the saved `deck` (with an `id`)
> * `readDeck(deckId, signal)`
> 	* Returns the `deck` with the matching `deckId`
> * `updateDeck(updatedDeck, signal)`
> 	* `updatedDeck` must have an `id` property
> 	* Returns the updated `deck`
> * `deleteDeck(deckId, signal)`
> 	* Returns an empty Object.
> * `listCards(deckId, signal)`
> 	* Returns an array of `cards` matching the `deckId`
> * `createCard(deckId, card, signal)`
> 	* `card` must not have an `id` property (the function will make one automatically)
> 	* Returns the saved `card` (with an `id`)
> * `readCard(cardId, signal)`
> 	* Returns the `card` with the matching `cardId`
> * `updateCard(updatedCard, signal)`
> 	* `updatedCard` must have an `id` property
> 	* Returns the updated `card`
> * `deleteCard(cardId, signal)`
> 	* Returns an empty Object.

### Example implementation with `listDecks`:
```javascript
const [decks, setDecks] = useState([]);
const abortController = new AbortController();
const signal = abortController.signal;

// get decks when first rendered.
useEffect(() => {
	getDecks();

	return () => {
		abortController.abort();
	};

	// eslint-disable-next-line react-hooks/exhaustive-deps
}, []);

/**
 * Fetches all of the current decks from the database.
 */
async function getDecks() {
	try {
		const response = await listDecks(signal);
		setDecks(response);
	}
	catch(error) {
		if(error.name !== "AbortError") {
			throw error;
		}
	}
}
```

---

## **6. Important Notes**
### `deck.cards` Array
The Qualified instructions do not mention this, but every `deck` has a `cards` array attached to it. You can choose whether you want to use the utility function `readCard()` or this method.
```javascript
deck.cards[0]; // access the first card of the deck
```

### `window.confirm()`
This will be used as a confirmation before deleting either a deck or a card. If the user presses "OK", the function will return `true`. If the user presses "Cancel", the function will return `false`.
```javascript
window.confirm(`Delete this deck?\n\nYou will not be able to recover it.`);
```

### `getParams()` return type
No matter what, `getParams` always returns a string.
```javascript
// example path: decks/:deckId
// example url: https://localhost:3000/decks/1
const { deckId } = useParams(); // deckId = "1", a string
```

### `parseInt()`
So, if we want to use a string as a number, we can use `parseInt`.
```javascript
const deckIdNumber = parseInt(deckId); // deckIdNumber = 1, a number
```

### Checking if Object is empty
```javascript
// we cannot do the following to check if an Object is empty:
if(deck === {}) // will compile but will always be false

// instead, we can check to see if the object has no keys:
if(Object(deck).keys.length === 0)
```

---

## **7. Passing the Qualified Tests**
*sigh.* This app is a big example of Qualified tests wanting you to implement things a very specific way. I created the app and got it fully functional, but then met with a TA and realized that all my tests were failing because of what the tests are looking for. If you are failing tests that you think should be passing, refer to the list below.

### Make sure you do the following when trying to pass these tests: *(aside from implementing what it is actually supposed to do)*
> landing on a bad page shows "Not Found" page
* Must use `listDecks`
* Must say "Not Found"
> route for /
* Must use `listDecks`
> route for /decks/:deckId
* Must use `readDeck`
> route for /decks/new
* Must use `<input>` once
* Must use `<textarea>` once
* Must say "Create Deck"
> route for /decks/:deckId/edit
* Must use `readDeck`
> route for /decks/:deckId/cards/new
* Must use `readDeck`
* Must say "Add Card"
> route for /decks/:deckId/cards/:cardId/edit
* Must use `readDeck`
* Must use `readCard`
> route for /decks/:deckId/study
* Must use `readDeck`
* Must say "Card 1 of 3" (with dynamic numbers)
* Must have a button that says "Flip"
* Must have a button that says "Next"
> route for /decks/:deckId/study clicking flip shows next button
* Must use `readDeck`
* Next button should not exist while on the front of a card
* Next button should exist while on the back of a card
> route for /decks/:deckId/study not enough cards
* Must use `readDeck`
* Must say "Not enouch cards"

---

