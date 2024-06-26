<script setup lang="ts">
import { defineComponent } from 'vue';
import low from './images/low.svg';
import high from './images/high.svg';
import limited from './images/limited.svg';

const iconList = {
    low,
    high,
    limited,
}

const props = defineProps<{
    icon: 'high' | 'limited' | 'low'
}>();

</script>

<template>
    <img inert :src='iconList[props.icon] || iconList.limited' />
</template>
