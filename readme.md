# List and Keys

## Rendering Multiple Elements

```javascript
function numberList() {
    const data = [1,2,3];
    const elements = data.map((item) => 
        // especially we use unqiue identifier as a key, but if we don't have an unique key, the last resort is using index.
        <li key={item.toString()}>{item}</li>
    )
    return (
        <ul>
            { elements }
        </ul>
    )
}
```

## Keys Must be unique among siblings

When we create two different arrays, we can use the same key.

```javascript

const sidebar = (
    <ul>
        { props.number.map((item) => 
            <li key={item.id}>{item.value}</li>
        )}
    </ul>
)

const titlebar = (
    <ul>
        {props.number.map((item) => 
            <li key={item.id}>{item.title}</li>
        )}
    </ul>
)

return (
    <div>
        {sidebar}
        {titlebar}
    </div>
)

```

### Embedding map in JSX

```js
function NumberList(props) {
    return (
        <ul>
            {
                numebrs.map((item) => 
                    <ListItem key={item.id} value={item.title} />
                )
            }
        </ul>
    )
}
```

## Extracing Compoennts with Keys

```javascript
function ListItem(props) {
    return (
        <li>{props.value}</li>
    )
}

function NumberList() {
    const number = [1,2];
    const listItems = number.map((item) => {
        <ListItem
            key={item.toString()}
            value={item}
        />
    })
    return (
        <ul>{listItems}</ul>
    )
}
// A good rule of thunmb is that elements inside the `map()` call need keys
```

# Conditional Rendering
```javascript
if(true) {
    return <h1>hello world</h1>
}
return <h1>hello world!</h1>
```

## Inline if

`true && expression`

```javascript
render() {
    return (
        data.length > 0 && <p>self-discipline and grit</p>
    )
}
```

## Inline if-else

`condition ? true: false`

```javascript
return (
    { isLogin ? 'Logout' : 'Login' }
)
```

```javascript
return (
    <div>
        {isLogin ? (
            <button onClick={this.handleLogOut}/>
        ): (
            <button onClick={this.handleLogIn}/>
        )}
    </div>
)
```

## Element Variables

Typically used for event handlers.
```javascript
class LoginButton extends React.Component {
    constuctor(props) {
        super(props);
    }

    render() {
        let button;
        if(isLogin) {
            button = <button onClick={this.handleLogOut}>Log out</button>
        } else {
            button = <button onClick={this.handleLogin}>Log in</button>
        }
        return (
            {button}
        )
    }
}

```

# Handling Events
## Passing Arguments to Event Hanlders

This is a common scenario especially in loop.

```javascript
const data = [1, 2, 3];
class App extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return (
            <div>
                {
                    data.length && data.map((item, key) => (
                        <button onClock={(e) => this.showItem(item, e)} key={key}>show</button>
                        /**
                        or
                            <button onClock={this.showItem.bind(this, e)} key={key}>show</button>
                        */
                    ))
                }
            </div>
        )
    }
}
```

# Forms

## Controlled Components

To have a js function that handles the submisson of the forms and has access to the data the user entered into the form.

Such as `form`, `input`, `textarea` typically has their own state and update based on user input. However, in `React`, mutable state is kept in `State`, and can only be updated via `setState`. Typically an `input form element` whose value is controlled by the React is called a `controlled component`.

```javascript
handleChange = (e) => {
    this.setState({
        value: e.target.value
    })
}

handleSubmit = (event) => {
    console.log(event.target.value);
    event.preventDefault();
}

render() {
    return (
        <form onSubmit={this.handleSubmit}>
            <input value={this.state.value} onChange={this.handleChange} />
        </form>
    )
}
```
With `controlled components`, we can modify or validate the user input.
For example, if we want to lowerCase the user input.
```javascript
handleChange = (event) => {
    this.setState({
        value: event.target.value.toLowerCase()
    });
}
```

## The textarea tag

Note that in HTML, `textarea` defines its content by its children.

```javascript
<textarea>children</textarea>
```

Whereas in React, a `textarea` uses a `value` attribute instead.

```javascript

constructor(props) {
    super(props);
    this.state = {
        value: 'hello wolrd'
    };
}

handleChange = (event) => {
    this.setState({
        value: e.target.value
    });
}

render() {
    return(
        <textarea value={this.state.value} onChange={this.handleChange} />
    )
}
```

## The select tag

In html, select tag works like below

```html
<select>
    <option value='coconut'>coconut</option>
    <option value='pen'>pen</option>
    <option value='book' selected>book</option>
</select>
```

Nevertheless, in React, the value is defined in the root of the select

```javascript
    <select value={this.state.value} onChange={this.handleChange}>
        <option value='coconut'>Coconut</option>
        <option value='pen'>Pen</option>
        <option value='book'>Book</option>
    </select>
```

Multiple options in a select tag

```javascript
<select multiple={true}  value={['a', 'c']}>
```

## Handling multiple inputs

We can add a `name` attribute to each input element, and let one handler function to choose what to do based on the name of the input element.


```javascript

    handleChange = (event) => {
        const name = event.target.name;
        const value = event.target.value;
        this.setState({
            [name]: value
        })
    }
    render() {
        return (
            <form>
                <input
                    name="sure"
                    value={this.state.onSure}
                    onChange={this.handleChange}
                />
                <input
                    name="cancle"
                    value={this.state.onCancle}
                    onChange={this.handleChange}
                />
            </form>
        )
    }

```



# Reference
[React Doc](https://reactjs.org/)