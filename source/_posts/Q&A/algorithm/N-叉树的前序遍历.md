---
title: N 叉树的前序遍历
date: 2022-08-24 20:13:45
tags: Q&A
categories:
- [Q&A, Q&A-algorithm]
---

## 题目
给定一个 n 叉树的根节点  root ，返回 其节点值的 前序遍历 。

n 叉树 在输入中按层序遍历进行序列化表示，每组子节点由空值 null 分隔（请参见示例）。


示例 1：
输入：root = [1,null,3,2,4,null,5,6]
输出：[1,3,5,6,2,4]


示例 2：
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[1,2,3,6,7,11,14,4,8,12,5,9,13,10]

## 题解
```
    class Node {
        public int val;
        public List<Node> children;

        public Node() {}

        public Node(int _val) {
            val = _val;
        }

        public Node(int _val, List<Node> _children) {
            val = _val;
            children = _children;
        }
    }

    public List<Integer> preorder(Node root) {
        List<Integer> integerList = new ArrayList<>();
        getOrder(root, integerList);
        return integerList;
    }

    void getOrder(Node root, List<Integer> integerList) {
        if (root == null) {
            return;
        }
        integerList.add(root.val);
        for (Node sonRoot :
                root.children) {
            getOrder(sonRoot, integerList);
        }
    }
```
