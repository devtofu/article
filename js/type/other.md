# js其他判断

## string 相关

### isNonBlankString

判断给定的值是否为` 非空字符串 `。如果是返回true，否则返回false。

```
function isNonBlankString(val) {
  return typeof val === 'string' && (/\S/).test(val);
}
```

### isBlankString

判断给定的值是否为` 空字符串 `。如果是返回true，否则返回false。

```
function isBlankString(val) {
  return typeof val === 'string' && val.trim().length === 0;
}
```

## element

### isEl

判断给定的值是否为` dom元素 `。如果是返回true，否则返回false。

```
function isEl(val) {
  return isObject(val) && val.nodeType === 1;
}
```

注：`isObject(val)`，请参考[`js type`](https://github.com/lvzhenbang/article/blob/master/learning/js.type.md#isobject)

### isTextNode

判断给定的值是否为` 文本节点 `。如果是返回true，否则返回false。

```
function isTextNode(val) {
  return isObject(val) && val.nodeType === 3;
}
```

注：`isObject(val)`，请参考[`js type`](https://github.com/lvzhenbang/article/blob/master/learning/js.type.md#isobject)


## iframe

### isInframe

判断给定的值是否为` Inframe元素 `。如果是返回true，否则返回false。

```
function isInFrame() {
  try {
    return window.parent !== window.self;
  } catch (x) {
    return true;
  }
}
```

注：在Safari中，如果获取`parent` 或 `self`，将抛出异常，因此需要使用`try/catch`。

## mouse

### isSingleLeftClick

判断是否为`鼠标左键单击`。如果是返回true，否则返回false。

```
function isSingleLeftClick(event) {
  if (event.button === undefined && event.buttons === undefined) {
    return true;
  }

  if (event.button === 0 && event.buttons === undefined) {
    return true;
  }

  if (event.button === 0 && event.buttons === 0) {
    return true;
  }

  if (event.button !== 0 || event.buttons !== 1) {
    return false;
  }

  return true;
}
```

注：参考来源[` isSingleLeftClick `](https://github.com/videojs/video.js/blob/master/src/js/utils/dom.js#L761)


## class

### hasClass

判断某元素` el ` 是否有类` clsName `。如果有返回true，否则返回false。

```
function hasClass(el, clsName) {
  clsName = clsName.trim()
  if (el.classList) {
    return el.classList.contains(clsName);
  }
  return (new RegExp('(^|\\s)' + clsName + '($|\\s)')).test(el.className);
}
```

## range

### isBottom

判断是否` 到达页面底部 `。如果是返回true，否则返回false。

```
funciton isBottom() {
  return document.documentElement.clientHeight + window.scrollY >=
  (document.documentElement.scrollHeight || document.documentElement.clientHeight);
}
```

### isTop

判断是否` 到达页面顶部 `。如果是返回true，否则返回false。

```
funciton isTop() {
  return (window.scrollY || document.documentElement.scrollTop) <= 0;
}
```

### elementIsVisibleInViewport

判断元素` el `是否出现在` 浏览器窗口 `。如果是返回true，否则返回false。

```
const elementIsVisibleInViewport = (el, partiallyVisible = false) => {
  const { top, left, bottom, right } = el.getBoundingClientRect();
  const { innerHeight, innerWidth } = window;
  return partiallyVisible
    ? ((top > 0 && top < innerHeight) || (bottom > 0 && bottom < innerHeight)) &&
        ((left > 0 && left < innerWidth) || (right > 0 && right < innerWidth))
    : top >= 0 && left >= 0 && bottom <= innerHeight && right <= innerWidth;
};
```

注：参考来源[` 30-second-code elementIsVisibleInViewport `](https://github.com/30-seconds/30-seconds-of-code#elementisvisibleinviewport-)