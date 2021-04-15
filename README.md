# Handy cheat sheet

### 1. [HTML] Validating a nth-digit number

    <input id="phone" type="text" name="phone" 
        maxlength="10" pattern="[0-9]{10}" 
        title="Please enter exactly 10 digits" required>

That will check for an integer (0-9) values with a maximum of 10 digits.


### 2. [HTML] Validating an email to require .{any_string} at the end

The "email" type on HTML only checks for an @ sign with any values on the end but does not consider the dot (.) before the domain extension (e.g. myemail@test.com).

This pattern will also check to require .{any_string} with a minimum of 2 characters at the end

    <input id="email" type="email" name="email"
        pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"
        title="Please enter a valid email" required>

### 3. [JS] Comparing JavaScript objects

I've searched a lot on this one but finally I got the most simple solution that worked on what I'm trying to achieve.

I just converted a JavaScript object or value to a JSON string and that's it:

    return JSON.stringify(baseObject) === JSON.stringify(comparedObject);

### 4. [CSS] Sticky div inside a CSS Grid layout

By default, using `position:sticky;` on any item in the Grid layout will not be sticking to the top of the viewport since CSS Grid item sizing algorithm has effectively sized the grid item to fill the height of the grid slot it has been placed in.

To resize the item to compute its height to be just enough to accommodate the element’s contents, we can use one of the following approach:

We can specify one of the following:
1. `align-self:` this property, when specified on a sticky element, tells the element how to align itself to the block direction of the grid slot it’s in. 
2. `align-self: start;` would work nicely in our example, as it will align the item to the “start” edge of the grid slot (in this context, the top edge).
3. `align-items:` this property, when specified on the parent grid, tells each grid item how to align itself to the block direction of the grid slot it’s in

Here is a sample working solution to see it in action:
    
    .post {
      display: grid;
      grid-template-columns: 20em 1fr;
      grid-gap: 4em;
    }

    .post__title {
      position: sticky;
      top: 0;
      align-self: start; /* The trick to autocompute the element's height so it would stick to the top of our viewport on scroll */
    }

Reference URL: [Sticky CSS Grid Items](https://melanie-richards.com/blog/css-grid-sticky/#how-to-fix-it)

**ANOTHER IMPORTANT NOTE THAT COULD SAVE YOU A LOT OF TIME DEBUGGING**
- You may encounter certain circumstances wherein the `position:sticky;` is still not working after doing all the things above.
- If so, look for an ancestor element that has an overflow that is set to hidden (`overflow:hidden;`). It may cause the sticky positioning to not work as expected. You may have to go up the DOM tree higher than you expected. I promise you. :p

Reference URL: [How does the “position: sticky;” property work?](https://stackoverflow.com/questions/43707076/how-does-the-position-sticky-property-work/47878455#47878455)


### 4. [JS] Make array of object render in random order

Use `.sort(() => Math.random() - .5)`.

Example:

    [
        { color: 'green', flipped: false, cleared: false },
        { color: 'red', flipped: false, cleared: false },
        { color: 'blue', flipped: false, cleared: false },
        { color: 'yellow', flipped: false, cleared: false },
        { color: 'green', flipped: false, cleared: false },
        { color: 'red', flipped: false, cleared: false },
        { color: 'blue', flipped: false, cleared: false },
        { color: 'yellow', flipped: false, cleared: false },
    ].sort(() => Math.random() - .5)

### 5. [JS] Conditionally adding keys to JavaScript objects using spread operators and short-circuit evaluation

In JavaScript, the && and || operators actually return the value of the last expression that gets evaluated in the statement.

Example:

    const buildAnObjectFromAQuery = query => ({
      ...query.foo && { foo: query.foo },
      ...query.bar && { bar: query.bar },
    });
    
In the above example, `query.foo && { foo: query.foo }` will return `{ foo: query.foo }` if `query.foo` is truthy, and will short-circuit to return false if `query.foo` is falsey.

Reference: https://medium.com/@mikeh91/conditionally-adding-keys-to-javascript-objects-using-spread-operators-and-short-circuit-evaluation-acf157488ede
