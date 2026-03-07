---
order: 1
title: Пузырьковая
---



Смысли проходимся по массиву двойным цмклом и сравниваем соседнием элементы ,

тем самым самый большой элемент встает в конец.

Пример go

```
package main

import "fmt"

func bubleSort(nums []int) {

	for i := 0; i < len(nums)-1; i++ {
		swapped := false
		for j := 0; j < len(nums)-1-i; j++ {
			if nums[j] > nums[j+1] {
				temp := nums[j+1]
				nums[j+1] = nums[j]
				nums[j] = temp
				swapped = true
			}
		}
		if swapped != true {
			break
		}
	}
}

func main() {
	nums := []int{3, 2, 1}
	bubleSort(nums)
	fmt.Println(nums)
}
```