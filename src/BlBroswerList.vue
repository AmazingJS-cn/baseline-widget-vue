<template>
    <div class="bl-title-broswer">
        <div class="bl-broswer-item" v-for="broswer in Object.keys(broswerList)" :key="broswer">
            <svg class="bl-b-icon" aria-hidden="true">
                <use :xlink:href="'#icon-' + broswer"></use>
            </svg>
            <svg v-if="broswerList[broswer] === true" class="bl-b-icon-check" aria-hidden="true">
                <use xlink:href="#icon-check"></use>
            </svg>
            <svg v-else-if="broswerList[broswer] === false" class="bl-b-icon-check" aria-hidden="true">
                <use xlink:href="#icon-error"></use>
            </svg>
            <span v-else class="bl-b-v">{{ broswerList[broswer] }}</span>
        </div>
    </div>
</template>


<script setup lang="ts">
import './images/iconfont';
import { ref } from 'vue';

export type BroswerSupportsType = {
    // broswerSupports: true
    // edge:true  chrome:116  firefox:false
    chrome?: string | number | boolean
    edge?: string | number | boolean
    safari?: string | number | boolean
    firefox?: string | number | boolean
} | boolean;

// 该组件可支持的参数
const props = withDefaults(defineProps<{
    broswerSupports?: BroswerSupportsType
}>(), {
    broswerSupports: true
});

// console.log(props.broswerSupports, typeof props.broswerSupports);

const broswerList = ref({
    chrome: true,
    edge: true,
    safari: true,
    firefox: true
});
if (props.broswerSupports === false) {
    broswerList.value = {
        chrome: false,
        edge: false,
        safari: false,
        firefox: false
    }
} else if (typeof props.broswerSupports === 'object') {
    for (let key in props.broswerSupports) {
        broswerList.value[key] = props.broswerSupports[key];
    }
}
// console.log(broswerList.value)

</script>

<style lang="less" scoped>
.bl-title-broswer {
    display: flex;
    gap: 7px;
    --bl-broswer-item-height: 25px;

    .bl-broswer-item {
        position: relative;
        line-height: var(--bl-broswer-item-height);
        height: var(--bl-broswer-item-height);
        background: rgb(210, 227, 252);
        display: inline-block;
        border-radius: 20px;
        font-size: 0;
        line-height: var(--bl-broswer-item-height);
        // padding: 0 8px 0 0;
        display: flex;
        align-items: center;

    }

    .bl-b-icon {
        width: var(--bl-broswer-item-height);
        height: var(--bl-broswer-item-height);
        fill: currentColor;
        overflow: hidden;
    }

    .bl-b-icon-check {
        width: calc(var(--bl-broswer-item-height)/2);
        height: calc(var(--bl-broswer-item-height)/2);
        fill: currentColor;
        overflow: hidden;
        position: absolute;
        right: -2px;
        bottom: 0;
        background: #fff;
        border-radius: 4px;
    }

    .bl-b-v {
        font-size: 14px;
        color: #555;
        padding: 0 8px 0 3px;
        line-height: 1;
    }
}

.bl-high-support {
    .bl-title-broswer .bl-broswer-item {
        background: rgb(199, 235, 206);
    }
}

.bl-limited-support {
    .bl-title-broswer .bl-broswer-item {
        background: rgb(241, 227, 175);
    }
}

.bl-dark-mode {
    .bl-b-icon-check {
        background: #152f5a;
    }

    .bl-b-v {
        color: #ccc;
    }

    .bl-title-broswer .bl-broswer-item {
        background: rgb(34, 70, 114);
    }

    &.bl-high-support {
        .bl-title-broswer .bl-broswer-item {
            background: rgb(11, 80, 25);
        }
    }

    &.bl-limited-support {
        .bl-title-broswer .bl-broswer-item {
            background: rgb(85, 68, 7);
        }
    }
}
</style>