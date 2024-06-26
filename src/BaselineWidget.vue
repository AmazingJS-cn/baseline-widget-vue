<template>
    <div class="bl-wrapper" :class="{
        'bl-dark-mode': dark,
        'bl-high-support': type === 'high',
        'bl-limited-support': type === 'limited'
    }">
        <BlIcon :icon="props.type" class="bl-icon"></BlIcon>
        <div class="bl-content-wrapper">
            <div class="bl-title">
                <div class="bl-title-text-wrapper">
                    <strong>Baseline</strong> {{ props.baseline }}
                    <span class="bl-title-text">{{ props.title }}</span>
                </div>
                <BlBroswerList :broswerSupports="props.broswerSupports"></BlBroswerList>
                <svg class="bl-fold-ctrl" :class="{ 'bl-fold-ctrl-up': !contentFolded }" v-if="showSlot && foldCtrl"
                    @click="toggleFold">
                    <use xlink:href="#icon-down"></use>
                </svg>
            </div>
            <div v-show="showSlot && !contentFolded" class="bl-content">
                <slot>{{ content }}</slot>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import './images/iconfont';
import { ref, computed, useSlots, defineProps } from 'vue';
import { type BroswerSupportsType } from './BlBroswerList.vue';
import BlIcon from './BlIcon.vue';
import BlBroswerList from './BlBroswerList.vue';

export type BaselineWidgetProps = {
    type?: 'high' | 'limited' | 'low'
    // 2023 '2024'
    baseline?: string | number
    title?: string
    content?: string
    showContent?: boolean
    // broswerSupports: true
    // edge:true  chrome:116  firefox:false
    broswerSupports?: BroswerSupportsType
    dark?: boolean
    fold?: boolean
    foldCtrl?: boolean
}

// 该组件可支持的参数
const props = withDefaults(defineProps<BaselineWidgetProps>(), {
    type: 'low',
    broswerSupports: true,
    fold: false,
    foldCtrl: true
});

const slots = useSlots();
const showSlot = ref(!!slots['default']);
const contentFolded = ref(props.fold);

// 在slot里面的所有内容均为空的时候，也要隐藏
if (slots.default && slots.default().every(i => {
    let slotType = (typeof i.type === 'symbol' ? String(i.type) : i.type);
    // 注释类型的节点
    if (slotType === 'Symbol(v-cmt)' || slotType === 'v-cmt' || slotType === 'comment') {
        return true;
    }
    return false;
})) {
    showSlot.value = false;
}

function toggleFold() {
    contentFolded.value = !contentFolded.value;
}

</script>

<style lang="less" scoped>
.bl-wrapper {
    font-family: Inter, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
    background: rgb(232, 240, 254);
    color: #333;
    border-radius: 6px;
    padding: 15px;
    min-width: 240px;
    font-size: 0;
    display: flex;
    align-items: flex-start;

    &.bl-high-support {
        background: rgb(229, 249, 233);
    }

    &.bl-limited-support {
        background: rgb(250, 244, 223);
    }

    &.bl-dark-mode {
        background: rgb(17, 42, 85);
        color: #fff;

        .bl-content {
            color: rgba(240, 240, 240, 0.7)
        }

        &.bl-high-support {
            background: rgb(8, 49, 16);
        }

        &.bl-limited-support {
            background: rgb(51, 41, 7);
        }

        .bl-fold-ctrl {
            fill: #fff;
        }
    }


}

.bl-icon {
    height: 18px;
    margin-top: 2.5px;
}

.bl-fold-ctrl {
    height: 10px;
    width: 10px;
    margin-top: 8px;
    margin-left: 5px;
    fill: #444;
    cursor: pointer;
    transition: all .2s;

    &.bl-fold-ctrl-up {
        transform: rotate(180deg);
    }
}

.bl-content-wrapper {
    flex: 1;
    font-size: 14px;
    margin-left: 10px;
}

.bl-title {
    display: flex;
    align-items: start;
    flex-wrap: wrap;
    gap: 5px;

    .bl-title-text-wrapper {
        container-type: inline-size;
        font-size: 16px;
        line-height: 1.5;
        margin: 0;
        margin-right: 10px;
        flex: 1;
        min-width: 125px;
    }
}

.bl-content {
    font-size: 16px;
    padding-top: 12px;
    padding-bottom: 5px;
    line-height: 1.5;
    color: rgba(60, 60, 60, 0.7);
}

@container (max-width: 255px) {
    .bl-title-text {
        display: none;
    }
}
</style>