# [React CountUp](https://glennreyes.github.io/react-countup)

[![Build Status](https://travis-ci.org/glennreyes/react-countup.svg?branch=master)](https://travis-ci.org/glennreyes/react-countup)
[![Coverage Status](https://coveralls.io/repos/github/glennreyes/react-countup/badge.svg?branch=master)](https://coveralls.io/github/glennreyes/react-countup?branch=master)
[![Dependency Status](https://david-dm.org/glennreyes/react-countup.svg)](https://david-dm.org/glennreyes/react-countup)
[![Dependency Status](https://david-dm.org/glennreyes/react-countup/dev-status.svg)](https://david-dm.org/glennreyes/react-countup#info=devDependencies)
[![npm version](https://badge.fury.io/js/react-countup.svg)](https://badge.fury.io/js/react-countup)

A configurable React component wrapper around [CountUp.js](https://inorganik.github.io/countUp.js/).

![sep -15-2016 10-11-53 pm](https://cloud.githubusercontent.com/assets/5080854/18565869/d23db0e0-7b91-11e6-9ee2-71be5875ca48.gif)

## Installation

```bash
yarn add react-countup
```

## Usage

```js
import CountUp from 'react-countup`;
```

#### Simple

```js
<CountUp end={160526} />
```

#### Advanced

```js
<CountUp
  className="account-balance"
  start={-875.039}
  end={160527.012}
  duration={2.75}
  separator=" "
  decimals={4}
  decimal=","
  prefix="EUR "
  suffix=" left"
  onEnd={() => console.log('Ended! 👏')}
  onStart={() => console.log('Started! 💨')}
>
  {({ countUpRef, start }) => (
    <div>
      <div ref={countUpRef} />
      <button onClick={start} />
    </div>
  )}
</CountUp>
```

## API

### Props

#### `autostart: number`

By default the transition will start automatically.

However, if CountUp is used as a render prop component, the transition will
automatically on initial render.

Default: `false`

> Note: Alternatively, you can also set `delay={0}` instead to automatically start the count up.

#### `className: string`

CSS class name of the span element.

> Note: This won't be applied when using CountUp with render props.

#### `decimal: string`

Specifies decimal character.

Default: `.`

#### `decimals: number`

Amount of decimals to display.

Default: `0`

#### `delay: number`

Delay in seconds before starting the transition.

Default: `null`

> Note: `delay={0}` will automatically start the count up.

#### `duration: number`

Duration in seconds.

Default: `2`

#### `end: number`

Target value.

#### `prefix: string`

Static text before the transitioning value.

#### `redraw: boolean`

Forces count up transition on every component update.

Default: `false`

#### `separator: string`

Specifies character of thousands separator.

#### `start: number`

Initial value.

Default: `0`

#### `suffix: string`

Static text after the transitioning value.

#### `useEasing: boolean`

Enables easing. Set to `false` for a linear transition.

Default: `true`

#### `easingFn: (t: number, b: number, c: number, d: number) => number`

Easing function. Click [here](http://robertpenner.com/easing) for more details.

Default: [`easeInExpo`](https://github.com/inorganik/countUp.js/blob/master/countUp.js#L103-L106)

#### `formattingFn: (value: number) => string`

Function to customize the formatting of the number

#### `onEnd: ({ pauseResume, reset, start, update }) => void`

Callback function on transition end.

#### `onStart: ({ pauseResume, reset, update }) => void`

Callback function on transition start.

#### `onPauseResume: ({ reset, start, update }) => void`

Callback function on pause or resume.

#### `onReset: ({ pauseResume, start, update }) => void`

Callback function on reset.

#### `onUpdate: ({ pauseResume, reset, start }) => void`

Callback function on update.

### Render props

#### `countUpRef: () => void`

Ref to hook the countUp instance to

#### `pauseResume: () => void`

Pauses or resumes the transition

#### `reset: () => void`

Resets to initial value

#### `start: () => void`

Starts or restarts the transition

#### `update: (newEnd: number?) => void`

Updates transition to the new end value (if given)

## Protips

By default, the animation is triggered if any of the following props has changed:

- `duration`
- `end`
- `start`

If `redraw` is set to `true` your component will start the transition on every component update.

## Examples

### Manually start the transition

Render start value but don't initially start transition:

```js
<CountUp end={100}>
  {({ countUpref, start }) => (
    <div>
      <span ref={countUpRef} />
      <button onClick={start}>Start</button>
    </div>
  )}
</CountUp>
```

Render start value and start transition:

```js
<CountUp autostart end={100}>
  {({ countUpref, start }) => (
    <div>
      <span ref={countUpRef} />
      <button onClick={start}>Start</button>
    </div>
  )}
</CountUp>
```

### Delay the transition

```js
<CountUp delay={5} end={100} />
```

## License

MIT
