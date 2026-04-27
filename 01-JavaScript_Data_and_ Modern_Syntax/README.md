### JavaScript Data and Modern Syntax

- Level: Beginner → Intermediate

# Welcome:

Welcome to Series 1: JavaScript Data & Modern Syntax.

In this series, you’ll learn how to read, transform, and safely manipulate data, the skill that everything else in frontend development depends on.

We’ll cover arrays, objects, and modern JavaScript features like destructuring, spread, and optional chaining, along with defensive coding patterns that help you avoid common bugs.

By the end, you’ll be able to handle real-world data with confidence, not just write code, but write code that holds up.

## Topic Clusters

- Arrays (iteration + transformation)
- Objects (structure + access)
- Modern syntax (destructuring, spread, optional chaining)
- Defensive coding patterns

## map() Arrays - transform arrays for real UIs

- Definition:
  map() walks through every item in an array, runs your function on it, and returns a brand-new array of the same length. It never changes the original.

- Syntax:
  version with function: array.map(function(currentValue, index, arr), this)
  version with arrow function: array.map((currentValue, index, arr))

  function(): Required. A function/callback function to be run for each array element
  currentValue: Required. The value of the current element
  index: Optional. The index of the current element
  arr: Optional. The array of the current element
  this: Optional. Default value is undefined. A value passed to the function to be used as its this value.

- Key takeaways:
  - Loop through every item in an array
  - Return / create a new array with the same length
  - does not change the original array

- Example:
  // We have products from an API
  const products = [
  { id: 1, name: "Wool Beanie", price: 24 },
  { id: 2, name: "Canvas Tote", price: 35 },
  { id: 3, name: "Cork Wallet", price: 18 },
  ];

  // map() turns each product into an HTML string
  const cards = products.map((product) => {
  return `<div class="card">

    <h3>${product.name}</h3>
        <p>£${product.price}</p>
    </div>`;
    });

  // cards is now an array of 3 HTML strings
  document.getElementById("list").innerHTML = cards.join("");

================================= END MAP() ===================================

## filter()

- Definition:
  filter() keeps every item that passes your test and returns an array(could be empty, could have many items).
- Syntax:
  version with function: array.filter(function(currentValue, index, arr), this)
  version with arrow function: array.filter((currentValue, index, arr))

  function(): Required. A function/callback function to be run for each array element
  currentValue: Required. The value of the current element
  index: Optional. The index of the current element
  arr: Optional. The array of the current element
  this: Optional. Default value is undefined. A value passed to the function to be used as its this value.

- Key takeaways:
  - The filter() method creates a new array filled with elements that pass a test provided by a function.
  - The filter() method does not execute the function for empty elements.
  - The filter() method does not change the original array.

- Example:
  const cartItems = [
  { id: 1, name: "Beanie", qty: 2, inStock: true },
  { id: 2, name: "Scarf", qty: 0, inStock: false },
  { id: 3, name: "Gloves", qty: 1, inStock: true },
  ];

  // filter() — get ALL in-stock items (returns array)
  const available = cartItems.filter((item) => item.inStock);
  // → [{Beanie}, {Gloves}]

================================= END FILTER() ===================================

## find()

- Definition:
  find() returns the first single item that matches, or undefined if nothing matches.

- Syntax:
  version with function: array.find(function(currentValue, index, arr), this)
  version with arrow function: find.map((currentValue, index, arr))

  function(): Required. A function/callback function to be run for each array element
  currentValue: Required. The value of the current element
  index: Optional. The index of the current element
  arr: Optional. The array of the current element
  this: Optional. Default value is undefined. A value passed to the function to be used as its this value.

- Key takeaways:
  - The find() method returns the value of the first element that passes a test.
  - The find() method executes a function for each array element.
  - The find() method returns undefined if no elements are found.
  - The find() method does not execute the function for empty elements.
  - The find() method does not change the original array.

- Example:
  const cartItems = [
  { id: 1, name: "Beanie", qty: 2, inStock: true },
  { id: 2, name: "Scarf", qty: 0, inStock: false },
  { id: 3, name: "Gloves", qty: 1, inStock: true },
  ];

  // find() — get ONE specific item by id (returns object or undefined)
  const scarf = cartItems.find((item) => item.id === 2);
  // → { id: 2, name: "Scarf", qty: 0, inStock: false }

  ================================= END FIND() ===================================

## Nullish coalescing operator (??)

- Definition:
  The nullish coalescing (??) operator is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.

- Syntax: leftExpression ?? rightExpression

- Key takeaways:
  - if the left operand is true, then its returned
  - if the left operand is false, then the right operand is operand.

- Example:
  let name = null;
  let text = "missing";
  let result = name ?? text;

- Example 2:
  // API returns this product object
  const products = [
  {
  id: 42,
  title: "Not Organic Cotton Tee",
  variants: [{ size: "S", stock: 3 }],
  // note: no "description" key at all
  },
  {
  id: 42,
  title: "Organic Cotton Tee",
  variants: [{ size: "M", stock: 5 }],
  description: "Here is the Organic Cotton Tee description",
  },
  ];
  const body = document.querySelector("body");
  body.innerHTML = products
  .map((product) => {
  const description = product.description ?? "Not description";
  return `<div class="w-[400px] flex flex-col gap-2 border border-gray-200 mb-5">
  <h2 class="font-lg font-semibold">${product.title}</h2>
        <div>
            <span class="border py-1 px-2">${product.variants[0].size}</span>
  <span class="border py-1 px-2">${product.variants[0].stock}</span>
        </div>
        <div class="text-red-600">${description}</div>
    </div>`;
  })
  .join("");

  ================================= END NULLISH COALESCING OPERATOR ===================================

## Destructuring - Unpacking objects and arrays

- Definiton:
  Desctructuring is syntax sugar for pulling values out of objects or arrays and assigning them to named variables in one line.

- Syntax:
  - for objects: let {value1, value2, } = someVariable -> Note that order does not matter here
  - for arrays: let [value1, value2] = someVariable -> Note that order matter here

- Example with objects:
  // Create an Object
  const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50
  };

  // Destructuring
  let {firstName, lastName} = person;

  --> We could also add more properties:
  let {firstName, lastName, country = "US"} = person;

  --> We could play with the object property alias:
  let {lastName:name} = person;

- Examples with Arrays:
  // Create an Array
  const fruits = ["Bananas", "Oranges", "Apples", "Mangos"];
  // Destructuring
  let [randomName0, randomName1, randomName2, randomName3] = fruits;

  --> We can skip array values using two or more commas:
  // Create an Array
  const fruits = ["Bananas", "Oranges", "Apples", "Mangos"];
  // Destructuring
  let [, , , randomName] = fruits; => It is will output "Mangos"

  --> We can pick up values from specific index locations of an array:
  // Create an Array
  const fruits = ["Bananas", "Oranges", "Apples", "Mangos"];
  // Destructuring
  let {[0]:fruit1 ,[1]:fruit2} = fruits;

  ================================= END DESCTRUCTURING ===================================

## Spread Operator - Copy, merge, update

- Definition:
  The spread operator expands an array or object into individual items. For arrays it copies elements; for objects it copies key-value pairs.

- Syntax: ...someVariable

- Example:
  const cart = {
  items: ["beanie", "scarf"],
  total: 59,
  currency: "GBP"
  };

  // --> Update one field without mutating
  const updatedCart = { ...cart, total: 84 };
  // cart.total is still 59 — untouched
  // updatedCart.total is 84

  // --> Add a new field
  const cartWithDiscount = { ...cart, discount: 10 };

  // --> Merge two objects — right side wins on conflict
  const defaults = { currency: "USD", tax: true };
  const userPrefs = { currency: "GBP" };
  const config = { ...defaults, ...userPrefs };
  // → { currency: "GBP", tax: true } — GBP wins

  // --> Spread array — add item immutably
  const items = ["beanie", "scarf"];
  const newItems = [...items, "gloves"];

================================= END SPREAD OPERATOR ===================================

## Optional Chaining

- Definition:
  The optional chaining (?.) operator accesses an object's property or calls a function. If the object accessed or function called using this operator is undefined or null, the expression short circuits and evaluates to undefined instead of throwing an error.
