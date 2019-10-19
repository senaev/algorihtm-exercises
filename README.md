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
