# Lottie Interactivity

# Requirements

This is a small library to add scrolling interactivity to your Lottie Animations. This can be used with the
[Lottie Web-Player Component](https://www.lottiefiles.com/web-player) or the
[Lottie Player](https://github.com/airbnb/lottie-web).

# Installation

## via yarn

```
yarn add @lottiefiles/lottie-interactivity
```

## via npm

```
npm install --save @lottiefiles/lottie-interactivity
```

## via cdn

```html
<script src="https://unpkg.com/@lottiefiles/lottie-interactivity@0.1.0/dist/lottie-interactivity.min.js"></script>
```

# Demo

Demos are showcased at https://lottiefiles.com/interactivity

The javascript code for the demo is available at codesandbox
https://codesandbox.io/s/lottie-interactivity-fyffj?file=/src/index.js

# Getting started

#### 1. Add a Lottie to html dom with an ID set to the div

```html
<lottie-player
  id="firstLottie"
  src="https://assets2.lottiefiles.com/packages/lf20_i9mxcD.json"
  style="width:400px; height: 400px;"
>
  {" "}
</lottie-player>
```

#### 2. Setup configuration

The name of the object ie: 'firstLottie' in this example is the ID set to the lottie web component on the html page.
This object takes an object named actions which consists of an array of objects. Multiple objects can be added into this
array and therefore multiple actions such as "seek", "stop" and "loop", can be set. Each object has a start and end
which is essentially a percentage for the height of the lottie container and is a value between 0 and 1.

```javascript
const animActions = {
  mode: 'scroll',
  firstLottie: {
    actions: [
      {
        start: 0,
        end: 1,
        type: 'seek',
        frames: [0, 300],
      },
    ],
  },
};
```

#### 3. Call the LottieInteractivity.create method and pass the configuration object as a parameter

```javascript
LottieInteractivity.create(animActions);
```

# Scroll effect relative to container

There may be situations where you would like to wrap the lottie player inside a container or just in general sync the
lottie scroll with a div on your page. In which case you may pass a container variable with the container id into the
action object as shown below.

```javascript
const animActions = {
  mode: 'scroll',
  firstLottie: {
    container: 'myContainerId',
    actions: [
      {
        start: 0,
        end: 1,
        type: 'seek',
        frames: [0, 300],
      },
    ],
  },
};
```

# Scroll effect with offset

If you would like to add an offset to the top of the container or player you may add an extra action object to the
array. As per the example config below, from 0 to 30% of the container, the lottie will be stopped and from 30% to 100%
of the container the lottie will be synced with the scroll.

```javascript
const animActions = {
  mode: 'scroll',
  firstLottie: {
    actions: [
      {
        start: 0,
        end: 0.3,
        type: 'stop',
        frames: [0],
      },
      {
        start: 0.3,
        end: 1,
        type: 'seek',
        frames: [0, 300],
      },
    ],
  },
};
```

# Scroll effect with offset and segment looping

In cases where you would like the animation to loop from a specific frame to a specific frame, you can add an additional
object to actions in which you can specifify the frames. In the example below, the lottie loops frame 150 to 300 once
45% of the container is reached.

```javascript
const animActions = {
  mode: 'scroll',
  firstLottie: {
    actions: [
      {
        start: 0,
        end: 0.3,
        type: 'stop',
        frames: [0],
      },
      {
        start: 0.3,
        end: 0.45,
        type: 'seek',
        frames: [0, 150],
      },
      {
        start: 0.45,
        end: 1,
        type: 'loop',
        frames: [150, 300],
      },
    ],
  },
};
```

# Play segments

If you would like to play the animation and loop it only from a certain frame to a certain frame, then you can utilize
the loop action and frames variable. The config below shows this example.

```javascript
const animActions = {
  mode: 'scroll',
  firstLottie: {
    actions: [
      {
        start: 0.45,
        end: 1,
        type: 'loop',
        frames: [17, 63],
      },
    ],
  },
};
```

# Play on hover

The play on hover feature is part of the [Lottie Web-Player](https://www.lottiefiles.com/web-player) library. Simply add
the hover prop to the player component as shown below.

```html
<lottie-player
  id="firstLottie"
  hover
  src="https://assets6.lottiefiles.com/packages/lf20_NQAN9S.json"
  style="width: 400px; height: 400px;"
></lottie-player>
```

# Play segments on hover

To loop certain segments on hover, ensure that the Lottie is already at the frame you want to start the on hover loop
from (Check the javascript code to find out how). Once thats done you can use the library's "hover" action to loop the
segment.

```javascript
const animActions = {
  mode: 'hover',
  firstLottie: {
    actions: [
      {
        start: 0,
        end: 1,
        type: 'seek',
        frames: [0, 139],
      },
    ],
  },
};
```

The next step is to add a "hover" action along with the frames you would like to loop from and to.

```javascript
const animActions = {
  mode: 'hover',
  firstLottie: {
    actions: [
      {
        start: 0,
        end: 1,
        type: 'seek',
        frames: [45, 60],
      },
    ],
  },
};
```
