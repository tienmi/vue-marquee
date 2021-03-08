# Feature

![Image of Vue-marquee-straight](https://upload.cc/i1/2021/03/08/mFIVX7.gif)

This is a vue-exclusive marquee component, which features an unlimited up and down carousel that will be connected end to end.

# Usage

### Install

```javascript
npm i @vue_modules/vue-marquee-straight
```

### Basic

import and register components

```javascript
import TheMarquee from "@vue_modules/vue-marquee-straight";
import "@vue_modules/vue-marquee-straight/marqueeBar.css";

export default {
  components: {
    TheMarquee,
  },
};
```

Let's move

```javascript
<TheMarquee>
  <template v-slot:childList>
    <div>The block you want to rotate</div>
  </template>
</TheMarquee>
```

### Props

| Prop      | Type   | Default | Value          | Description                                                                            |
| --------- | ------ | ------- | -------------- | -------------------------------------------------------------------------------------- |
| direction | String | up      | 'up' or 'down' | Decide the direction of rotation                                                       |
| speed     | Number | 0       | -N ~ N         | Rotation speed, positive number means acceleration, negative number means deceleration |
