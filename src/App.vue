<script setup lang="ts">
import { ref } from 'vue'
import VueSliderInput from './components/VueSliderInput.vue'

const priceOptions = ref(['$0', '$10', '$20', '$30', '$40', '$50'])

const selectedValue1 = ref<number>(4) // Index for the selected value
const selectedValue2 = ref<number>(3)
const selectedValue3 = ref<number>(1)
const selectedValue4 = ref<number>(2)
</script>

<template>
    <div class="slider-display">
        <div class="slider-container">
            <VueSliderInput 
                :priceInput="priceOptions" 
                v-model="selectedValue1"
                :sliderColor="'#FF7582'" 
                :tooltipTextColor="'#FFFFFF'"
                :thumbColor="'#FFFFFF'"
                :showBreakpoints="true" 
                :breakPointColor="'#909cb5'" />
            <br>
            <br>
            <VueSliderInput 
                :priceInput="priceOptions" 
                v-model="selectedValue2"
                :sliderColor="'#C56D86'" 
                :tooltipTextColor="'#FFFFFF'"
                :thumbColor="'#355C7D'"
                :thumbColorInner="'#2A3950'"
                :showBreakpoints="false" />
            <p>The price is: <strong>{{ priceOptions[selectedValue2] }}</strong></p>
        </div>
        <div class="slider-container">
            <VueSliderInput 
                :priceInput="priceOptions" 
                v-model="selectedValue3"
                :sliderColor="'#C56D86'" 
                :tooltipBackgroundColor="'#121212'"
                :tooltipTextColor="'#FFFFFF'"
                :thumbColor="'#121212'"
                :thumbColorInner="'#121212'"
                :showBreakpoints="true" 
                :breakPointColor="'#909cb5'" />
            <br>
            <br>
            <VueSliderInput 
                :priceInput="priceOptions" 
                v-model="selectedValue4"
                :sliderColor="'#355C7D'"
                :tooltipBackgroundColor="'#F5F5F5'" 
                :tooltipTextColor="'#212121'"
                :thumbColor="'#FFFFFF'"
                :showBreakpoints="false" />
            <p>The price is: <strong>{{ priceOptions[selectedValue4] }}</strong></p>
        </div>
    </div>
</template>

<style scoped>
.slider-display {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    @media only screen and (max-width: 1200px) {
        flex-direction: column;
    }
} 
.slider-container {
    max-width: 90vw;
    width: 520px;
    margin: 20px;
}
</style>
