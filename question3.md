vue面试第三题：
        你知道vue中key的作用和工作原理吗？说说你对它的理解。

​		答：Vue中没有key属性的话，会默认使用“就地复用”策略，也即是列表中的 数据顺序发生改变时，不会移动dom元素，只是更新相应元素的内容节点。毋庸置疑，这种方式能提高性能，此模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

​	使用 `key`，它会基于 `key` 的变化重新排列元素顺序，并且会移除 `key` 不存在的元素。
 它也可以用于强制替换元素/组件而不是重复使用它。当你遇到如下场景的时候它可能会很有用:

- 完整地触发组件的生命周期钩子
- 触发过渡



vue源码中：

```javascript
// 如果有带 key
  if (isUndef(oldKeyToIdx)) {
    // 创建 index 表
    oldKeyToIdx = createKeyToOldIdx(oldCh, oldStartIdx, oldEndIdx);
  }
  if (isDef(newStartVnode.key)) {
    // 有 key ,直接从上面创建中获取
    idxInOld = oldKeyToIdx[newStartVnode.key]
  } else {
    // 没有key, 调用 findIdxInOld
    idxInOld = findIdxInOld(newStartVnode, oldCh, oldStartIdx, oldEndIdx);
  }
```

可以看出主要是createKeyToOldIdx和findIdxInOld两个函数的比较

```javascript
function createKeyToOldIdx (children, beginIdx, endIdx) {
  let i, key
  const map = {}
  for (i = beginIdx; i <= endIdx; ++i) {
    key = children[i].key
    if (isDef(key)) map[key] = i
  }
  return map
}
```



```javascript
 function findIdxInOld (node, oldCh, start, end) {
    for (let i = start; i < end; i++) {
      const c = oldCh[i]
      if (isDef(c) && sameVnode(node, c)) return i
    }
  }
```



从上面的代码可以看出，如果我们有 `key` 值，就可以直接在 `createKeyToOldIdx` 方法中创建的 `map` 映射表中根据 `key` 值，找到相应的值。没有 `key` 值，则需要遍历才能拿到。相比于遍历，映射的速度会更快。

**`key` 值是每一个 `vnode` 的唯一标识，依靠 `key`，我们可以更快的拿到 `oldVnode` 中相对应的节点。**