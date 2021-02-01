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

![image-20210128115259066](https://github.com/fxfzxxx/Notes/blob/master/images/1611806423(1).jpg?raw=true)

#### Delete all files in the `src/` folder of the new project.

#### Add `index.js` to the folder:

```react
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';

class Square extends React.Component {
    render() {
      return (
        <button className="square">
          {/* TODO */}
        </button>
      );
    }
  }
  
  class Board extends React.Component {
    renderSquare(i) {
      return <Square />;
    }
  
    render() {
      const status = 'Next player: X';
  
      return (
        <div>
          <div className="status">{status}</div>
          <div className="board-row">
            {this.renderSquare(0)}
            {this.renderSquare(1)}
            {this.renderSquare(2)}
          </div>
          <div className="board-row">
            {this.renderSquare(3)}
            {this.renderSquare(4)}
            {this.renderSquare(5)}
          </div>
          <div className="board-row">
            {this.renderSquare(6)}
            {this.renderSquare(7)}
            {this.renderSquare(8)}
          </div>
        </div>
      );
    }
  }
  
  class Game extends React.Component {
    render() {
      return (
        <div className="game">
          <div className="game-board">
            <Board />
          </div>
          <div className="game-info">
            <div>{/* status */}</div>
            <ol>{/* TODO */}</ol>
          </div>
        </div>
      );
    }
  }
  
  // ========================================
  
  ReactDOM.render(
    <Game />,
    document.getElementById('root')
  );
  
```

#### Add `index.css` to the folder:

```css
body {
    font: 14px "Century Gothic", Futura, sans-serif;
    margin: 20px;
  }
  
  ol, ul {
    padding-left: 30px;
  }
  
  .board-row:after {
    clear: both;
    content: "";
    display: table;
  }
  
  .status {
    margin-bottom: 10px;
  }
  
  .square {
    background: #fff;
    border: 1px solid #999;
    float: left;
    font-size: 24px;
    font-weight: bold;
    line-height: 34px;
    height: 34px;
    margin-right: -1px;
    margin-top: -1px;
    padding: 0;
    text-align: center;
    width: 34px;
  }
  
  .square:focus {
    outline: none;
  }
  
  .kbd-navigation .square:focus {
    background: #ddd;
  }
  
  .game {
    display: flex;
    flex-direction: row;
  }
  
  .game-info {
    margin-left: 20px;
  }
  
```

#### Run `npm start`.

<center>
    <img style="border-radius: 0.3125em; zoom:80%;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://raw.githubusercontent.com/fxfzxxx/MD-Images/master/20210128171914.png">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Run npm start.</div>
</center>

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://raw.githubusercontent.com/fxfzxxx/MD-Images/master/20210128171950.png">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Open it in a browser.</div>
</center>

### Passing Data Through Props

#### 3 React components:

Square:  render `<button>` 

Boarder: render 9 squares.

Game: game logic

#### The flow of classes

Game invoke Boarder and the Boarder invokes Square. 

<center>
    <img style="border-radius: 0.3125em; zoom:80%;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://raw.githubusercontent.com/fxfzxxx/MD-Images/master/20210128225333.png">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">HTML Structure</div>
</center>

```react
  ReactDOM.render(
    <Game />,
    document.getElementById('root')
  );
```

Code above initialized  the app.

### Making an Interactive Component

Add `onClick` function:

```react
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() { alert('click'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

Seems like the class name square controls the onClick behaviour. Only button with square class can show the alert.

```react
class Square extends React.Component {
 render() {
   return (
     <button className="square" onClick={() => alert('click')}>
       {this.props.value}
     </button>
   );
 }
}
```

This introduced arrow function that I learnt like a month a ago.

To make the number becomes "X" after click it, the `state` is introduced. It's initialized in the subclass constructor and is a private value.

```react
constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }
```

All the component classes have to call `super(props)` in the first line of constructor.

```react
 render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
```

`setState` will re-render Square when the button is clicked. Up to this step, the initial value in the square is null instead of numbers. As it's showing `this.state.value` 

<center class="half">
    <img style="border-radius: 0.3125em; zoom:80%;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://raw.githubusercontent.com/fxfzxxx/MD-Images/master/20210128235302.png">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">Before click</div>
</center>

<center class="half">
    <img style="border-radius: 0.3125em; zoom:80%;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://raw.githubusercontent.com/fxfzxxx/MD-Images/master/20210128235355.png">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">After random clicks</div>
</center>







   <center class="half">

