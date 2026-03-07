---
order: 4
title: Сортировка слиянием
---

```
package main

import "fmt"

func mergeSort(nums []int) []int {

	if len(nums) <= 1 {
		return nums
	}

	midle := len(nums) / 2
	left := nums[:midle]
	right := nums[midle:]

	leftSorted := mergeSort(left)
	rightSorted := mergeSort(right)

	return merge(leftSorted, rightSorted)
}

func merge(left []int, right []int) []int {
	result := make([]int, 0, len(left)+len(right))

	i := 0
	j := 0
	for i < len(left) && j < len(right) {
		if left[i] < right[j] {
			result = append(result, left[i])
			i++
		} else {
			result = append(result, right[j])
			j++
		}
	}
	// Добавляем оставшиеся элементы (если есть)
	result = append(result, left[i:]...)
	result = append(result, right[j:]...)

	return result
}

func main() {
	nums := []int{3, 2, 1, 5, 10}

	fmt.Println(mergeSort(nums))
}
```