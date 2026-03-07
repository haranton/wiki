---
order: 1
title: Бинарное дерево
---

```

package main

import (
	"container/list"
	"fmt"
)

type Node struct {
	value int
	left  *Node
	right *Node
}

type Tree struct {
	root *Node
}

func (tree *Tree) Insert(value int) {
	tree.root = insert(tree.root, value)
}

func insert(searchNode *Node, value int) *Node {

	if searchNode == nil { // Базовый случай

		return &Node{
			value: value,
		}

	}

	if searchNode.value < value {
		searchNode.right = insert(searchNode.right, value)
	} else if searchNode.value > value {
		searchNode.left = insert(searchNode.left, value)
	}

	return searchNode

}

func (tree *Tree) Preorder() {
	preorder(tree.root)
}

func preorder(node *Node) {
	if node == nil {
		return
	}
	fmt.Print(node.value, " ")
	preorder(node.left)
	preorder(node.right)

}

func (tree *Tree) Inorder() {
	inorder(tree.root)
}

func inorder(node *Node) {
	if node == nil {
		return
	}
	inorder(node.left)
	fmt.Print(node.value, " ")
	inorder(node.right)

}

func levelOrder(root *Node) {
	if root == nil {
		return
	}

	q := list.New()
	q.PushBack(root)

	for q.Len() > 0 {
		elem := q.Front()
		q.Remove(elem)
		node := elem.Value.(*Node)

		fmt.Print(node.value, " ")

		if node.left != nil {
			q.PushBack(node.left)
		}

		if node.right != nil {
			q.PushBack(node.right)
		}
	}
}

func main() {

	tree := Tree{}

	// arr := []int{5, 6, 3, 7, 2, 4}
	arr := []int{5, 6, 3, 7, 2, 4}
	for _, value := range arr {
		tree.Insert(value)
	}

	levelOrder(tree.root)
}

```



### **Виды обхода** 

### В глубину (рекурсия)

1) Узел - правый - левый 

2) правый - Узел -  левый 

3) правый - левый Узел

В ширину (очередь) 


