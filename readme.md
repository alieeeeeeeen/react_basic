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

# Reference
[React Doc](https://reactjs.org/)