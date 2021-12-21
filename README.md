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
