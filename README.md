# algorihtm-exercises

## bubble sort

```javascript
(nums) => {
    for (let i = nums.length; i > 0; i--) {
        for (let k = 0; k < i; k++) {
            const current = nums[k];
            if (current > nums[k + 1]) {
                nums[k] = nums[k + 1];
                nums[k + 1] = current;
            }
        }
    }
    
    return nums;
}
```

## selection sort

```javascript
(nums) => {
    const { length } = nums;

    for (let i = 0; i < length - 1; i++) {
        let minIntex = i;

        for (let k = i + 1; k < length; k++) {
            if (nums[k] < nums[minIntex]) {
                minIntex = k;
            }
        }

        const min = nums[minIntex];
        nums[minIntex] = nums[i];
        nums[i] = min;
    }
    
    return nums;
}
```

## insertion sort

```javascript
(nums) => {
    const { length } = nums;

    for (let i = 1; i < length; i++) {
        let k = i;
        const next = nums[k];

        while (k > 0 && nums[k - 1] > next) {
            nums[k] = nums[k - 1];
            k--;
        }

        nums[k] = next;
    }
    
    return nums;
}
```

## n-array tree preorder traversal

```javascript
(root) => {
    const arr = [];
    
    if (!root) {
        return arr;
    }
    
    const traverseChild = (node) => {
        arr.push(node.val);
        
        node.children.forEach(traverseChild);
    }
    
    traverseChild(root);
    
    return arr;
}
```

## n-array tree level order traversal

```javascript
const x = {
    val: 1,
    children: [
        {
            val: 2,
            children: [
                {
                    val: 4,
                    children: [
                        {
                          val: 5,
                          children: []
                        },
                        {
                          val: 6,
                          children: []
                        },
                    ]
                }
            ]
        },
        {
          val: 3,
          children: []
        },
    ]
};

((root) => {
    const arr = [];
    
    if (!root) {
        return arr;
    }

    const traverseLevel = (roots) => {
        const nextLevel = [];
        arr.push(roots.map(({val, children}) => {
            nextLevel.push(...children)
            return val;
        }));

        if (nextLevel.length) {
            traverseLevel(nextLevel);
        }
    };

    traverseLevel([root]);

    return arr;
})(x)
```

##valid parentheses

###1

```javascript
function(s) {
    while (true) {
        const nextStr = s
            .replace('()', '')
            .replace('{}', '')
            .replace('[]', '');
        
        if (nextStr.length === 0) {
            return true;
        }
        
        if (nextStr.length === s.length) {
            return false;
        }
        
        s = nextStr;
    }
}
```

###2

```javascript
function(s) {
    const stack = [];
    
    const open = '([{';
    const close = ')]}';
    
    for (let i = 0; i < s.length; i++) {
        const sym = s[i];
        
        const openIndex = open.indexOf(sym);
        const closeIndex = close.indexOf(sym);

        if (openIndex > -1) {
            stack.push(openIndex);
        } else if (closeIndex > -1) {
            if (stack.length === 0) {
                return false;
            }
            
            const lastInStack = stack[stack.length - 1];
            
            if (closeIndex !== lastInStack) {
                return false;
            }

            stack.pop();
        }
    }
    
    return stack.length === 0;
};
```

## show all primes from one to N

```javascript
(n) => {
    const arr = [];
    const primes = []

    for (let i = 2; i < n; i++) {
        let j = 2;

        if (arr[i] === undefined) {
            primes.push(i);
        }

        while (j * i < n) {
            arr[j * i] = 1;
            j++;
        }
    }

    return primes.length;
}
```

## binary search

```javascript
function(nums, target) {
    let left = 0;
    let right = nums.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) {
            return mid;
        }

        if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;
}
```

## revert linked list

```
cocnst list = {
  value: 1,
  next: {
    value: 2,
    next: {
      value: 3,
      next: {
        value: 4,
        next: null
      }
    }
  }
};

function(head) {
    let prev = null;
    while (head) {
        const { next } = head;
        head.next = prev;

        prev = head;
        head = next;
    }
    
    return prev;
}
```

### find all permutations

```javascript
(nums) => {
    if (nums.length === 1) {
        return [nums];
    }

    const numsPermutationsArray = [];
    
    
    for (let i = 0; i < nums.length; i++) {
        const otherNumbers = nums.slice(0, i).concat(nums.slice(i + 1));

        const childPermutations = findPermutations(otherNumbers);

        for (let k = 0; k < childPermutations.length; k++) {
            numsPermutationsArray.push([nums[i], ...childPermutations[k]])
        }
    }
    
    return numsPermutationsArray;
}
```

## array max sum partition

```javascript
function (arr) {
    let partSum = 0;
    let maxSum = 0;

    for (const val of arr) {
        partSum += val;
        maxSum = Math.max(partSum, maxSum);

        if (partSum < 0) {
            partSum = 0;
        }
    }

    return maxSum;
}

[1, 2, 3, 4, 5, 6, -100, 3, 4, 5, 6, 7] = 25
[] = 0
[-1, -2, -1, 1, -4, 5, -1, 7, -6, -1] = 11
```

## spiral square martix

```javascript
function (n) {
    const getNumber = (x, y) => {
        return n * x + y + 1;
    }

    const circle = (size) => {
        if (size === 1) {
            return [[0, 0]];
        }

        const arr = [];
        for (let i = 0; i < size; i++) {
            arr.push([0, i]);
        }
        for (let i = 1; i < size - 1; i++) {
            arr.push([i, size - 1]);
        }
        
        const { length } = arr;
        for (let i = 0; i < length; i++) {
            arr.push([size - arr[i][0] - 1, size - arr[i][1] - 1]);
        }

        return arr;
    };

    const nums = []
    for (let i = 0; i < n; i += 2) {
        const offset = i / 2;
        const coords = circle(n - i);
        
        for (let [x, y] of coords) {
            nums.push(getNumber(x + offset, y + offset));
        }
    }

    return nums;
}

0 = []
1 = [1]
2 = [1,2,4,3]
3 = [1,2,3,6,9,8,7,4,5]
4 = [1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10]
5 = [1,2,3,4,5,10,15,20,25,24,23,22,21,16,11,6,7,8,9,14,19,18,17,12,13]
6 = [1,2,3,4,5,6,12,18,24,30,36,35,34,33,32,31,25,19,13,7,8,9,10,11,17,23,29,28,27,26,20,14,15,16,22,21]
100 = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15, ...... ,4852,4952,5052,5152,5151,5150,5149,5049,4949,4950,4951,5051,5050]
```

## merge sorting

```javascript
(nums) => {
    const sortParts = (first, second) => {
        const result = [];
        let firstPartIndex = 0;
        let secondPartIndex = 0;
        
        const resultLength = first.length + second.length;
        for (let i = 0; i < resultLength; i++) {
            const f = first[firstPartIndex];
            const s = second[secondPartIndex];

            if (f === undefined || f > s) {
                result.push(s);
                secondPartIndex++;
            } else {
                result.push(f);
                firstPartIndex++;
            }
        }
        
        return result;
    }
    
    let start = 0;
    let length = 1;
    while (length < nums.length) {
        while (start < nums.length) {
            const left = nums.slice(start, start + length);
            const right = nums.slice(start + length, start + length * 2);

            const sorted = sortParts(left, right); 
            
            nums.splice(start, length * 2, ...sorted);

            start += length * 2;
        }
        
        length *= 2;
        start = 0;
    }
    
    return nums;
};
```
