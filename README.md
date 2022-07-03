
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