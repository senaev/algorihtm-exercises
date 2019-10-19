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
