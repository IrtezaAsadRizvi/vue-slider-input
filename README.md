# Vue Slider Input


![[banner]](https://i.ibb.co/CKTgxgt/vue-slider-input.png)


VueSliderInput is a highly customizable and user-friendly slider component for Vue 3, designed to enhance user experience with interactive and visually appealing sliders. This versatile slider component comes with a tooltip feature, making it ideal for applications requiring precise input and feedback, such as pricing selections, age selection, and more.

## ✨ Demo
Try the slider out! - **<a href="https://vue-slider-input.web.app/" target="_blank">vue-slider-input.web.app</a>**

## ✨ Features

- ✨ **Tooltip Display**: Provides real-time feedback by displaying the current slider value in a tooltip, improving user interaction.
- ✨ **Customizable Appearance**: Allows you to customize slider colors, tooltip colors, and thumb colors to match your application’s theme.
- ✨ **Breakpoints**: Optionally display breakpoints along the slider for better user guidance.
- ✨ **Flexible Input**: Accepts an array of predefined values, perfect for fixed pricing tiers or predefined age ranges.
- ✨ **Responsive Design**: Ensures smooth performance and visual consistency across various screen sizes and devices.



## 🎯 install

```bash
npm install vue-slider-input --save
```

## 🚀 Usage

Import and Use 
```html
<script setup lang="ts">
import { ref } from 'vue'
import VueSliderInput from 'vue-slider-input'

const priceOptions = ref(['$0', '$10', '$20', '$30', '$40', '$50'])

const selectedValue = ref<number>(0) // index of selected value

</script>

<template>
    <VueSliderInput 
        :priceInput="priceOptions" 
        v-model="selectedValue"
        :sliderColor="'#FF7582'" 
        :tooltipTextColor="'#FFFFFF'"
        :thumbColor="'#FFFFFF'"
        :showBreakpoints="true" 
        :breakPointColor="'#909cb5'" />
</template>
```
![[image]](https://i.ibb.co/VNW9jjG/vue-input-slider-demo.png)

## Customization
### prop properties

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `priceInput` | `Array<string>` | `[]` | Array of String which would populate the slider. |
| `sliderColor` | `string` | `"#4CAF50"` | Color of the slider. |
| `tooltipTextColor` | `string` | `"#FFFFFF"` | Color of the Tooltip text. |
| `tooltipBackgroundColor` | `string` | `sliderColor` | Background color of the Tooltip. |
| `thumbColor` | `string` | `"#FFFFFF"` | Color of the Thumb/Handle. |
| `thumbColorInner` | `string` | `sliderColor` | Color of the dot inside the Thumb/Handle. |
| `showBreakpoints` | `boolean` | `false` | Whether to show the breakpoints. |
| `breakPointColor` | `string` | `"#909cb5"` | Color of the breakpoints. |


## License

[MIT]