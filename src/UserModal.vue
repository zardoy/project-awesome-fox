<script setup lang="ts">
import { computed, toRefs } from 'vue';
import IconClose from './IconClose.vue'
import { type UserType } from './types';

const props = defineProps<{
    isOpen: boolean,
    user?: UserType
}>()
const { isOpen, user } = toRefs(props)
defineEmits(['update:isOpen'])

const staticInfoRows = computed(() => [
    ['Phone', user?.value?.phone],
    ['Email', user?.value?.email],
    ['Hire date', user?.value?.hire_date],
    ['Position name', user?.value?.position_name],
    ['Department', user?.value?.department],
] as const)
</script>
<template>
    <div v-if="isOpen" class="container">
        <div class="root">
            <div class="header">
                <h2 class="name">{{ user!.name }}</h2>
                <IconClose class="close-icon" @click="$emit('update:isOpen', false)" />
            </div>
            <div class="info-block">
                <div class="info-block-rows-column">
                    <div v-for="row in staticInfoRows" :key="row[0]" class="info-row">
                        <div class="regular-text">{{ row[0] }}</div>
                    </div>
                </div>
                <div class="info-block-rows-column">
                    <div v-for="row in staticInfoRows" :key="row[0]" class="info-row">
                        <div class="text-muted info-block-text-content">{{ row[1] }}</div>
                    </div>
                </div>
            </div>
            <div class="more-info-block">
                <div class="regular-text">
                    More info
                </div>
                <div class="text-muted additional-information">
                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Deleniti eligendi repellat magni quod
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped lang="scss">
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    inset: 0;
    background: rgba(188, 195, 208, 0.5);
}

.root {
    display: flex;
    flex-direction: column;
    width: 500px;
    height: 468px;
    padding: 24px;
    gap: 40px;
    flex-shrink: 0;
    border-radius: 16px;
    background: #FFF;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.10);
}

.header {
    display: flex;
    justify-content: space-between;
}

.name {
    font-size: 24px;
    font-style: normal;
    font-weight: 700;
    line-height: 30px;
}

.close-icon {
    cursor: pointer;
}

.info-block {
    display: flex;
    gap: 40px;
    align-self: stretch;
}

.info-block-rows-column {
    display: flex;
    flex-direction: column;
    gap: 14px;
}

.regular-text {
    /* Text 18/24 */
    font-size: 18px;
    font-style: normal;
    font-weight: 400;
    line-height: 24px;
}

.info-block-text-content {
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 18px;
}

.text-muted {
    color: var(--Asphalt, #8189A3);
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 24px
}

.more-info-block {
    display: flex;
    flex-direction: column;
    gap: 12px;
}

.additional-information {
    line-clamp: 3;
}
</style>
