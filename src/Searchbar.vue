<script setup lang="ts">
import IconSearch from './IconSearch.vue';

const { modelValue } = defineProps<{
    modelValue: string;
}>()
defineEmits(['update:modelValue'])
</script>
<template>
    <div class="root">
        <input class="input" :value="modelValue"
            @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)">
        <div class="icon-container">
            <IconSearch class="icon" />
        </div>
    </div>
</template>
<style scoped lang="scss">
.root,
.input {
    width: 100%;
}

.root {
    position: relative;
}

.input {
    padding: 0 12px;
    height: 48px;
    border: 1px solid #D4DEFE;
    border-radius: 24px;
    flex-shrink: 0;
}

.icon-container {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.icon {
    margin-right: 24px;
}
</style>
