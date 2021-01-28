# Overview

### What is React

JavaScript library for building user interfaces.

Components is isolated pieces of code for complex UI. 

React.Component subclass **(JSX)** example:

```javascript
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

Component will tell React what to show on the screen.

If data changes, React will re-render the component.

This **React component class** use parameter called **props** and has a method **render()**. render( ) will return a **React Element**.

**At building time**, the  **<div />**  can be re-write to:

```javascript
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

---

### Inspecting the Starter Code

Under the project folder, bash input:

```shell
npx create-react-app my-app
```

![image-20210128115259066](C:\Users\Aaron\AppData\Roaming\Typora\typora-user-images\image-20210128115259066.png)