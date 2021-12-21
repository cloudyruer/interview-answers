# 1. Manipulate Private Array

## Function

```javascript
const test = () => {
  const arr = [];

  return {
    push(num) {
      arr.push(num);
      this.getArr();
    },

    pop() {
      arr.pop();
      this.getArr();
    },

    getArr() {
      console.log(arr);
    },
  };
};

const testObj = test();

testObj.push(1); // [1]
testObj.push(2); // [1,2]
testObj.push(3); // [1,2,3]
testObj.pop(); // [1,2]
```

## ES6 Class

```javascript
class testClass {
  arr = [];

  push(num) {
    this.arr.push(num);
    this.getArr();
  }

  pop() {
    this.arr.pop();
    this.getArr();
  }

  getArr() {
    console.log(this.arr);
  }
}

const classObj = new testClass();

classObj.push(1); // [1]
classObj.push(2); // [1,2]
classObj.push(3); // [1,2,3]
classObj.pop(); // [1,2]
```

# 2. Debounce - Resize

## With Closure (customized)

```javascript
const resizeHandler = (time = 500) => {
  let timerId;

  return (e) => {
    clearTimeout(timerId);
    timerId = setTimeout(() => {
      console.log(e.target.innerWidth);
    }, time);
  };
};

// 可將所需debounce時間填入客製化，預設為500ms
window.addEventListener("resize", resizeHandler(1000)); // 設定為1s
```

## Using bind (customized)

```javascript
let timerId2;
const resizeHandler2 = function (e) {
  clearTimeout(timerId2);
  timerId2 = setTimeout(() => {
    console.log(e.target.innerWidth);
  }, this || 500);
};
// 可將所需debounce時間填入客製化，預設為500ms
window.addEventListener("resize", resizeHandler2.bind(1000)); // 設定為1s
```

## React (hook)

```javascript
useEffect(() => {
  // Search Debouncing
  const timerId = setTimeout(() => {
    console.log("Do Something!");
  }, 1000);

  return () => clearTimeout(timerId);

  // 依據目標決定
}, [keyword]);
```

# 3. This

```javascript
console.log(this); // window

const getArrowThis = () => {
  console.log(this); // window, since arrow function (lexical)
};

const getFunThis = function () {
  console.log(this); // window, would be undefined in strict mode

  return {
    normalFun() {
      console.log(this); //obj

      (() => {
        console.log(this); // obj, lexical
      })();
    },
    arrowFun: () => {
      console.log(this); // window, would be undefined in strict mode (lexical)
    },
  };
};

getArrowThis();

const obj = getFunThis();
obj.normalFun();
obj.arrowFun();
```

# 4. CSS - Center

```html
<body class="way1">
  <div class="way2">This is my div</div>
</body>
```

```css
* {
  margin: 0;
  padding: 0;
}

body {
  height: 100vh;
  position: relative;
}

div {
  width: 100px;
  height: 100px;
  background-color: aqua;
}

body.way1 {
  display: flex;
  align-items: center;
  justify-content: center;
}

div.way2 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

# 5. flex-basis & flex-grow

```html
<body>
  <div class="demo demo--basis"></div>
  <div class="demo demo--grow"></div>
</body>
```

```css
* {
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}

.demo {
  width: 100px;
}

.demo--basis {
  background-color: blue;
  /* 看想要多高囉 */
  flex-basis: 100px;
}

.demo--grow {
  background-color: red;
  flex-grow: 1;
}
```
