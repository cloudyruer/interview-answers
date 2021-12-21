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
