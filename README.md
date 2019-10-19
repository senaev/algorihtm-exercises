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
