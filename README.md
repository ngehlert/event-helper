# Event Helper

This is a small Helper Library that helps you with adding and removing EventListeners in your application.

## Usage

### Setup

Install via npm
```
npm install @ngehlert/event-helper
```

Best used with ES6 imports
```javascript
import { EventHelper } from '@ngehlert/event-helper';
```

### Base usage
```javascript
EventHelper.addEventListener('my-event', document, 'keydown', (event) => {
    console.log(event);
    // do something here
});

// To remove the event listener simply call remove function with your specified name
EventHelper.removeEventListener('my-event');
```

### Usage with method specific context inside a class

```typescript
class MyTestClass {

    constructor() {
        EventHelper.addEventListener('my-event', document, 'keydown', this.myEventListenerFunction.bind(this));
    }
    
    private myEventListenerFunction(event: Event): void {
        // function that uses some class properties
    }
}
```

### One Time Event

After executing once the event listener automatically de-registers itself
```javascript
EventHelper.oneTimeEventListener(document, 'keydown', (event) => {
    console.log(event);
    // do something here
});
```

## Advantages
Easy listener management with names. In plain JavaScript the event handling can get quite messy, especially if you need methods with specific context (e.g. `.bind(this)`).  
With this event helper you can just use functions directly and while declaring the event add `.bind(this)` without needing to create a second variable.

Another advantage is if you want to remove the event not in the same spot where you registered it, you don't need to pass the proper reference along just to cancel the event.
```javascript
// Standard JavaScript way
const myMethod = (event) => {
  // do something
}
const myMethodListener = myMethod.bind(this);

document.addEventListener('mousedown', myMethodListener);
document.removeEventListener('mousedown', myMethodListener);
```

## Development
To build
```
npm run build
```

Before commiting run
```
npm run lint && npm run format && npm run test
```

## License
This is provided under the MIT license. Check LICENSE file for more details.
