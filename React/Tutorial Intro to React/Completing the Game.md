# Completing the Game

### Lifting State Up

In the parent board class, use array to store the value of "X", "O" or null. So, the Square Classes can be marked by the same array with different index. In other words, they can communicate.

```react
class Board extends React.Component {
      constructor (props) {
          super(props);
          this.state = {
              square: Array(9).fill(null),
          }
      }
    renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }
```

Define the handClick function in board class:

```react
handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = 'X';
    this.setState({squares: squares});
  }
```

### Function Components

Function components only have render method without state.

```react
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

this. keyword removed because it's no longer a class. And arrow function removed.

### Taking Turns

In the constructor, Initialize "X" to be the first move:

```react
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

In the click function, fill in the Array with "X" or "O", flip it every filling.

```react
handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

### Declaring a Winner

```react
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

This is the algorithm of game. Still not sure about the && === syntax. And why does it return a null value.

```react
handleClick(i) {
        const squares = this.state.squares.slice(); // copy
        if (calculateWinner(squares)||squares[i]) {
            return;
        }
        squares[i] = this.state.xIsNext ?'X':'O';
        this.setState({
            squares: squares,
            xIsNext: !this.state.xIsNext,
        });
    }
```

In the above function, the return words with nothing will stop the function and no go forward to execute the 6-11 lines code.



