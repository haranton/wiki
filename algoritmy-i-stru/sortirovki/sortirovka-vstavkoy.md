---
order: 2
title: "Сортировка выбором\_"
---

Смысл пройтись массиву найти самый маленький элемент и вставить в начало 

```
package main

import "fmt"

func insertSort(nums []int) {

	for i := 0; i < len(nums)-1; i++ {
		if i == len(nums)-2 {
			continue
		}
		min := i
		for j := i; j < len(nums)-1; j++ {
			if nums[min] > nums[j+1] {
				min = j + 1
			}
		}

		temp := nums[i]
		nums[i] = nums[min]
		nums[min] = temp

	}
}

func main() {
	nums := []int{3, 2, 1, 5, 10}
	insertSort(nums)
	fmt.Println(nums)
}
```