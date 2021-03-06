
## 1. [useState](#useState)
## 2. [useEffect](#useEffect)


<a name="useState"></a>

# useState

### Step1. Firstly, let's see how to use the useState in React formlly.

``` javascript

import React, { useState } from 'react';
const [state, setState] = useState(initialState);

```

### Step2. Hence we know that the useState function will return an array including two values. The first value is the target state and second one is the corresponding setState function.

```javascript

let memorizedState;
function useState(initialValue) {
    // ...
    return [memorizedState, setState];
}

```

### Step3. Furthermore, let's realize the details simply.

```javascript

function render () {
    // ...
}

let memorizedState;
function useState(initialValue) {
    memorizedState = initialValue || state;
    function setState(newValue) {
        memorizedState = newValue;
        render();
    }
    return [memorizedState, setState];
}

```

### Step4. Nevertheless, we can execute the useState several times in one application. So how to reach this? The answer is that hooks are not magic but only arrays.

```javascript

function render () {
    // ...
}

let memorizedState = [];
let curIndex = 0;
function useState(initialValue) {
    memorizedState[curIndex] = initialValue || state;
    function setState(newValue) {
        memorizedState[curIndex] = newValue;
        render();
    }
    return [memorizedState[curIndex++], setState];
}

```

<a name="useEffect"></a>

# useEffect

### Step1. Similarly, let's see how to use the useEffect in React formlly.

``` javascript

import React, { useState, useEffect } from 'react';

function Clock() {
    const [count, setCount] = useState(0);
    useEffect(()=>{
        console.log(`Show ${count} times.`);
    });
    return (
        <div> Clock Component. Totally {count} times.</div>
    );
}

```

### Step2. As we saw above, useEffect function has a callback parameter and this callback will be executed.

``` javascript

function useEffect(callback) {
    callback();
}

```

### Step3. The useEffect function can have a second parameter which should be an array standing for the dependencies. Meanwhile, we should also consider the multiple times to execute useEffect.

``` javascript

let effectQueue = [];
let index = 0;
function useEffect(callback, deps) {
    if (Array.isArray(deps)) {
        return 'The second parameter should be array.';
    } else if (!deps)) {
        callback();
    } else {
        const prevDeps = effectQueue[index];
        const hasChanged = deps.every((dep, index) => {
            return !(dep === prevDeps[index]);
        });
        if (hasChanged) {
            callback();
        }
        effectQueue[index] = deps;        
    }
    index++;
}

```