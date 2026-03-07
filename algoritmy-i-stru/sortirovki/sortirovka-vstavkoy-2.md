---
order: 3
title: Сортировка вставкой
---



Смысл в том чтобы идти  назад и искать место для элемента

у нас в начале есть отсортированный массив с 1 элемента

```
package main
import "fmt"
func insertionSort(arr []int) {
	for i := 1; i < len(arr); i++ {
		key := arr[i]   // текущий элемент, который вставляем
		j := i - 1
		// пока j >= 0 и элемент слева больше key — сдвигаем вправо
		for j >= 0 && arr[j] > key {
			arr[j+1] = arr[j]
			j--
		}
		// вставляем key на освободившееся место
		arr[j+1] = key
	}
}
func main() {
	arr := []int{3, 2, 1}
	fmt.Println("До сортировки:", arr)
	insertionSort(arr)
	fmt.Println("После сортировки:", arr)
}
```