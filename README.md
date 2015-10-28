## Split.js

[![Build Status](https://travis-ci.org/nathancahill/Split.js.svg?branch=v0.4.4)](https://travis-ci.org/nathancahill/Split.js)
[![File Size](https://badge-size.herokuapp.com/nathancahill/Split.js/master/split.min.js.svg?compression=gzip&label=size)](https://raw.githubusercontent.com/nathancahill/Split.js/master/split.min.js)

Split.js is a lightweight, unopinionated utility for creating adjustable split views or panes. [Demo](http://nathancahill.github.io/Split.js/).

No dependencies or markup required, just two or more elements with a common parent. Views can be split horizontally or vertically, with draggable gutters inserted between every two elements.

## Installation

Install with Bower:

```shell
bower install split.js
```

Or clone from Github:

```shell
git clone https://github.com/nathancahill/Split.js.git
```

## Documentation

```js
Split(<id[]> element ids, <options> options?)
```

| Options | Type | Default | Description |
|---|---|---|---|
| sizes | Array | | Initial sizes of each element in percents or CSS values. |
| minSize | Number or Array | 100 | Minimum size of each element. |
| gutterSize | Number | 10 | Gutter size in pixels. |
| snapOffset | Number | 30 | Snap to minimum width offset in pixels. |
| direction | String | 'horizontal' | Direction to split: horizontal or vertical. |
| onDrag | Function | | Callback on drag. |
| onDragStart | Function | | Callback on drag start. |
| onDragEnd | Function | | Callback on drag end. |

## Usage Examples

A split with two elements, starting at 25% and 75% wide with 200px minimum width.

```js
Split(['one', 'two'], {
    sizes: [25, 75],
    minSize: 200
});
```

A split with three elements, starting with even widths with 100px, 100px and 300px minimum widths, respectively.

```js
Split(['one', 'two', 'three'], {
    minSize: [100, 100, 300]
});
```

A vertical split with two elements.

```js
Split(['one', 'two'], {
    direction: 'vertical'
});
```

Specifying the initial widths with CSS values. Not recommended, the size/gutter calculations would have to be done before hand and won't scale on viewport resize.

```js
Split(['one', 'two'], {
	sizes: ['200px', '500px']
});
```

## CSS

In being non-opionionated, the only CSS Split.js sets is the widths or heights of the elements. Everything else is left up to you. However, here's some basic CSS to style the gutters with:

```css
.gutter {
  background-color: #eee;

  background-repeat: no-repeat;
  background-position: 50%;

  cursor: move;
  cursor: grab;
  cursor: -moz-grab;
  cursor: -webkit-grab;
}

.gutter:active { 
  cursor: grabbing;
  cursor: -moz-grabbing;
  cursor: -webkit-grabbing;
}

.gutter.gutter-horizontal {
  background-image: url('grips/vertical.png');
}

.gutter.gutter-vertical {
  background-image: url('grips/horizontal.png');
}
```

Split.js also works best when the elements are sized using `border-box`. The `split` class would have to be added manually to apply these styles:

```css
.split {
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
```

And for horizontal splits, floating the elements with 100% height is useful:

```css
.split, .gutter.gutter-horizontal {
  height: 100%;
  float: left;
}
```

Overflow can be handled as well:

```css
.split {
  overflow-y: auto;
  overflow-x: hidden;
}
```

## Browser Support

This library uses [calc()](https://developer.mozilla.org/en-US/docs/Web/CSS/calc#AutoCompatibilityTable), [box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing#AutoCompatibilityTable) and [getBoundingClientRect()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect#AutoCompatibilityTable). This features are supported in the following browsers:

| <img src="http://i.imgur.com/dJC1GUv.png" width="48px" height="48px" alt="Chrome logo"> | <img src="http://i.imgur.com/o1m5RcQ.png" width="48px" height="48px" alt="Firefox logo"> | <img src="http://i.imgur.com/8h3iz5H.png" width="48px" height="48px" alt="Internet Explorer logo"> | <img src="http://i.imgur.com/iQV4nmJ.png" width="48px" height="48px" alt="Opera logo"> | <img src="http://i.imgur.com/j3tgNKJ.png" width="48px" height="48px" alt="Safari logo"> |
|:---:|:---:|:---:|:---:|:---:|
| 19+ ✔ | 4+ ✔ | 9+ ✔ | 32+ ✔ | 7+ ✔ |

Gracefully falls back in IE 8 and below to only setting the initial widths/heights and not allowing dragging.