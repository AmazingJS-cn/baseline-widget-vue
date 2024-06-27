<script setup lang="ts">
import BaselineWidget from '@/BaselineWidget.vue';
const broswer = {
    safari: false,
    edge: 112,
    chrome: 160
}
const broswer2 = {
    chrome: true,
    safari: false,
    edge: false,
    firefox: false
}
</script>

<template>
    <div class="light">
        <div class="wrapper">
            <BaselineWidget type="high" baseline="2023" title="Newly available across major browsers"></BaselineWidget>
            <br>
            <BaselineWidget baseline="2024" title="Newly available across major browsers" :broswerSupports="broswer">
                Since April 2023, this feature works across the latest devices and browser versions. This feature might
                not
                work in older devices or browsers.
            </BaselineWidget>
            <br>
            <BaselineWidget type="limited" baseline="2024" title="Not supported by most browsers"
                :broswerSupports="broswer2">
            </BaselineWidget>
        </div>
    </div>

    <div class="dark">
        <div class="wrapper">
            <BaselineWidget dark type="high" baseline="2023" title="Newly available across major browsers">
                <slot></slot>
            </BaselineWidget>
            <br>
            <BaselineWidget dark baseline="2024" title="Newly available across major browsers"
                :broswerSupports="broswer">
                Since April 2023, this feature works across the latest devices and browser versions. This feature might
                not
                work in older devices or browsers.
            </BaselineWidget>
            <br>
            <BaselineWidget dark type="limited" baseline="2024" title="Not supported by most browsers"
                :broswerSupports="broswer2">
            </BaselineWidget>
        </div>
    </div>

</template>

<style scoped>
.wrapper {
    margin: auto;
    width: 80%;
    max-width: 800px;
}

.dark {
    background: #000619;
}

.dark,
.light {
    padding: 50px;
}
</style>
