# React Notes

## components

- React components are JavaScript functions that return markup
- a piece of the UI with its own logic and appearance

## JSX

JSX is the name for react markup syntax

HTML port to JSX? use an [online converter](https://transform.tools/html-to-jsx).

```
function SomeButton() {
  return (
    <button>I'm a button</button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <SomeButton />
    </div>
  );
}

```

### notes components

1. declare `function`
2. function (component) name must begin with UPPER CASE
3. html tags within JSX must be lower case
4. `return ()` always put parens after `return` for multi line.
5. html must be enclosed by a parent tag. `<> ... </>` is common.
6. `export default` maximum of 1 per module (js file)
7. `<SomeButton />` note self closing
8. `return (...);` ended with `;`
9. single tags must be closed `<img />` `<br />`

## Props
(properties) are how you pass data from one component to another in React, usually from a parent component to a child.

They make components resuable.

| Concept                                        | Explanation                                                                                |
| -----------------------------------------------| ------------------------------------------------------------------------------------------ |
| Props are read-only                            | You **can’t change** a prop in the child component. Think of props as function parameters. |
| Passed like HTML attributes                    | Just like you’d write `<img src="url" />`, you write props like `<Greeting name="Satchmo" />`. |
| Can be strings, numbers, objects, functions .. | Props are just JavaScript values.                                                              |
| You can rename in the function                 | Instead of `props.name`, you can write: `function Greeting({ name }) { ... }`                  |

```
function UserCard({ name, age, isAdmin }) {
  return (
    <div>
      <p>{name} ({age})</p>
      {isAdmin && <p>Admin</p>}
    </div>
  );
}

function App() {
  return (
    <UserCard name="Muna" age={30} isAdmin={true} />
  );
}
```

## CSS style

In React, you specify a CSS class with `className`.

`<img className="avatar" />`

## Displaying data

JSX lets you put markup into JavaScript. Curly braces let you “escape back” into JavaScript so that you can embed some variable from your code and display it to the user. to display `user.name`

```
return (
  <h1>
    {user.name}
  </h1>
);
```

You can also “escape into JavaScript” from JSX attributes, but you have to use curly braces instead of quotes. For example, `className="avatar"` passes the `"avatar"` string as the CSS class, but `src={user.imageUrl}` reads the JavaScript `user.imageUrl` variable value, and then passes that value as the src attribute:

```
return (
  <img
    className="avatar"
    src={user.imageUrl}
  />
);
```

```
const user = {
  name: 'Hedy Lamarr',
  imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
  imageSize: 90,
};

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={'Photo of ' + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize
        }}
      />
    </>
  );
}
```

1. `user` is an object with key:value pairs
2. `Profile()` is the component, rendered `<Profile />`
3. note `style={{key:value.attribute }} The inner {} is an object
4. You can use the `style` attribute when your styles depend on JavaScript variables.

## Conditionals

## Render lists

`for` loop and array `map()`

```
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
];
```

```
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);

return (
  <ul>{listItems}</ul>
);
```

1. `<li>` has a key attribute.
2. For each item in a list, pass a string or a number that uniquely identifies that item among its siblings. Usually, a key should be coming from your data, such as a database ID. React uses your keys to know what happened if you later insert, delete, or reorder the items.

## Event handlers

respond to events by declaring event handler functions inside your components

```
function MyButton() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```
1. note `onClick={handleClick}` has no parentheses at the end! Do not call the event handler function: you only need to pass it down. React will call your event handler when the user clicks the button.




## Questions and Answers

Q: is it true to say that, in JSX, a tag has attributes either defined by a string in quotes or javascript with curly braces?
that is, are there only those two options?

A: Yes, in JSX, an attribute value can be set in 1 of 2 ways:

String in quotes:
This passes a literal string value to the attribute.
`<img className="avatar" />`

JavaScript expression in curly braces:
This allows you to use any valid JavaScript expression (variable, function call, object, etc.) as the value.
`<img src={user.imageUrl} />`

These are the only two options for setting attribute values in JSX. You cannot use unquoted values or other syntaxes. If you want to use a number, object, boolean, or any dynamic value, you must use curly braces. For static strings, you use quotes.

---

Q: must any component include the word `return` in the function?

A: Yes, in React, a functional component must include the `return` statement to render any JSX or markup. The return statement specifies what the component should display on the screen.

```
function MyComponent() {
  return (
    <div>Hello, world!</div>
  );
}
```

If you omit return, the component will render nothing (i.e., it will return `undefined`). For multi-line JSX, always use parentheses after return for clarity and to avoid errors.

If you use an arrow function with an implicit return, you can omit the return keyword, but the function must still return JSX

```
const MyComponent = () => (
  <div>Hello, world!</div>
);
```

## Terms and Concepts
### Javascript Values
1. primitives
2. objects

### Primitive Values

simple, immutable and NOT objects

| Type          | Example                                        |
| ------------- | ---------------------------------------------- |
| **Number**    | `42`, `3.14`, `-10`                            |
| **String**    | `"hello"`, `'world'`                           |
| **Boolean**   | `true`, `false`                                |
| **Undefined** | `undefined` (a variable that has no value yet) |
| **Null**      | `null` (intentional empty value)               |
| **BigInt**    | `123456789012345678901234567890n`              |
| **Symbol**    | `Symbol('id')` (used for unique identifiers)   |

Object Values

more complex data structures

| Type                | Example                        |
| ------------------- | ------------------------------ |
| **Object**          | `{ name: "Satchmo", age: 40 }` |
| **Array**           | `[1, 2, 3]`                    |
| **Function**        | `function greet() { ... }`     |
| **Date**            | `new Date()`                   |
| **Class instances** | `new SomeClass()`              |


