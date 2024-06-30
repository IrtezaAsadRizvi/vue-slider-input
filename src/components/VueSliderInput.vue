<template>
    <div class="vue-slider">
        <label class="form-slider">
            <div class="slider-container">
                <input ref="slider" v-model="internalValue" type="range"
                    @input="handleSliderValuePosition($event.target)">
                <div class="vue-slider-tick" :style="{ borderTopColor: tooltipBackgroundColor || sliderColor }"
                    ref="sliderTick">
                    <div ref="sliderValue" class="vue-slider-value" :class="alignment"
                        :style="{ backgroundColor: tooltipBackgroundColor || sliderColor, color: tooltipTextColor }">
                        {{ getToolTipText(priceInput) }}
                    </div>
                </div>
            </div>
        </label>
        <div v-if="showBreakpoints" class="breakpoints">
            <span v-for="(value, index) in priceInput" :key="index" class="breakpoint"
                :style="{ color: breakPointColor }">
                {{ value }}
            </span>
        </div>
    </div>
</template>

<script setup>
import { ref, watch, onMounted, defineProps, defineEmits } from 'vue'

const props = defineProps({
    label: String,
    priceInput: Object,
    modelValue: [String, Number, Object, Array],
    sliderColor: {
        type: String,
        default: '#4CAF50' // default color if not provided
    },
    showBreakpoints: {
        type: Boolean,
        default: true
    },
    breakPointColor: {
        type: String,
        default: '#909cb5'
    },
    tooltipTextColor: {
        type: String,
        default: null // default to null, will handle default in style binding
    },
    tooltipBackgroundColor: {
        type: String,
        default: null // default to null, will handle default in style binding
    },
    thumbColor: {
        type: String,
        default: null // default to null, will handle default in style binding
    },
    thumbColorInner: {
        type: String,
        default: null // default to null, will handle default in style binding
    }
})

const emit = defineEmits(['update:modelValue'])

const internalValue = ref(props.modelValue ?? 0)
const thumbSize = ref(0)
const alignment = ref('center')
const slider = ref(null)
const sliderTick = ref(null)
const sliderValue = ref(null)

const tooltipTextColor = props.tooltipTextColor || props.breakPointColor
const tooltipBackgroundColor = props.tooltipBackgroundColor || props.sliderColor
const thumbColorInner = props.thumbColorInner || props.sliderColor
const thumbColor = props.thumbColor || '#FFFFFF'

const initiateSlider = () => {
    slider.value.setAttribute('min', 0)
    slider.value.setAttribute('max', props.priceInput.length - 1)
    handleSliderValuePosition(slider.value)
}

const handleSliderValuePosition = (input) => {
    emit('update:modelValue', internalValue.value)
    const sliderWidth = input.getBoundingClientRect().width - 20
    const multiplier = input.value / input.max
    const left = sliderWidth * multiplier
    const valueWidth = sliderValue.value.getBoundingClientRect().width
    alignment.value = left > (sliderWidth - valueWidth) ? 'right' : left < valueWidth ? 'left' : 'center'
    sliderTick.value.style.left = left + 'px'
}

const getToolTipText = (obj, pos) => {
    return pos !== undefined ? obj[props.modelValue] : obj[internalValue.value]
}

watch(() => props.modelValue, (newValue) => {
    internalValue.value = newValue
})

onMounted(() => {
    initiateSlider()
})
</script>

<style scoped>
.vue-slider {
    width: 100%;
    position: relative;
    margin-bottom: 30px;
}

.vue-slider .form-slider {
    display: block;
}

.vue-slider .form-slider span {
    display: block;
    text-align: left;
    margin-bottom: 16px;
    font-weight: 600;
    font-size: 1.375em;
    line-height: 27px;
    color: #212121;
}

.vue-slider .slider-container {
    border-radius: 10px;
    position: relative;
    margin-top: 40px;
}

.vue-slider .slider-container input {
    -moz-appearance: none;
    -webkit-appearance: none;
    border-radius: 10px;
    height: 12px;
    width: 100%;
    background-color: v-bind('sliderColor');
    outline: none;
}

.vue-slider .slider-container input::-webkit-slider-thumb {
    appearance: none;
    -webkit-appearance: none;
    background-color: v-bind('thumbColorInner');
    background-position: center;
    background-repeat: no-repeat;
    border: 5px solid v-bind('thumbColor');
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
    border-radius: 50%;
    cursor: pointer;
    height: 22px;
    width: 22px;
}

.vue-slider .slider-container input::-moz-range-thumb {
    background-color: v-bind('thumbColorInner');
    background-position: center;
    background-repeat: no-repeat;
    border: 5px solid v-bind('thumbColor');
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
    border-radius: 50%;
    cursor: pointer;
    height: 26px;
    width: 26px;
}

.vue-slider .slider-container input::-ms-thumb {
    background-color: v-bind('thumbColorInner');
    background-position: center;
    background-repeat: no-repeat;
    border: 5px solid v-bind('thumbColor');
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
    border-radius: 50%;
    cursor: pointer;
    height: 26px;
    width: 26px;
}

.vue-slider .slider-container input::-moz-focus-outer {
    border: 0;
}

.vue-slider .vue-slider-tick {
    position: absolute;
    display: block;
    width: 0;
    height: 0;
    border-style: solid;
    border-top: 10px solid v-bind('sliderColor');
    border-right: 10px solid transparent;
    border-left: 10px solid transparent;
    border-bottom: 0;
    position: absolute;
    bottom: 25px;
}

.vue-slider .vue-slider-value {
    position: absolute;
    font-size: 22px;
    font-weight: 600;
    color: #909cb5;
    margin-top: 8px;
    --thumb-size: 26px;
    background: v-bind('sliderColor');
    color: #fff;
    padding: 6px 10px 4px 10px;
    border-radius: 4px;
    bottom: 8px;
    left: 50%;
    transform: translateX(-50%);
}

.vue-slider .vue-slider-value.left {
    transform: translateX(-20%);
}

.vue-slider .vue-slider-value.right {
    transform: translateX(-80%);
}

.breakpoints {
    margin-top: 10px;
    display: flex;
    justify-content: space-between;
}

.breakpoint {
    font-size: 12px;
}
</style>