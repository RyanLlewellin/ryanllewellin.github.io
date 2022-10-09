# ReactJs Quick Start

## Components
- A component is a peice of the UI that contains its own logic
- JavaScript functions that return markup
- React component names must always start with a capital letter

``` javascript
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```
- Now I can use this component in another component
``` javascript
export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

## Styles
### Using CSS classNames
``` javascript
<img className="avatar" />
```
- In a CSS file:
``` javascript 
/* In your CSS */
.avatar {
  border-radius: 50%;
}
```