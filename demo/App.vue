<script setup lang="ts">
import BaselineWidget from '@/BaselineWidget.vue';
const broswer = {
    safari: false,
    edge: 112,
    chrome: 160
}
const broswer2 = {
    safari: false
}
</script>

<template>
    <div class="wrapper">
        <BaselineWidget dark type="high" baseline="2023" title="Newly available across major browsers"
            :broswerSupports="broswer">
            <!-- Since April 2023, this feature works across the latest devices and browser versions. This feature might not
            work in older devices or browsers. -->
        </BaselineWidget>
    </div>
</template>

<style scoped>
.wrapper {
    margin: 40px auto;
    width: 80%;
    max-width: 800px;
}
</style>
