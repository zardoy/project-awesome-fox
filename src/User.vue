<script setup lang="ts">
import { toRefs } from 'vue';
import IconPhone from './IconPhone.vue';
import IconMailbox from './IconMailbox.vue';
import { type UserType } from './types';

type ItemProps = Pick<UserType, 'name' | 'phone' | 'email'>
const { data } = defineProps<{
    data: ItemProps;
}>()
const { name, phone, email } = toRefs(data)
</script>

<template>
    <div class="container">
        <h2 class="title">
            {{ name }}
        </h2>
        <div class="info-block">
            <div class="info-block-row">
                <IconPhone />
                <span class="info-block-text">{{ phone }}</span>
            </div>
            <div class="info-block-row">
                <IconMailbox />
                <span class="info-block-text">{{ email }}</span>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.container {
    display: flex;
    flex-direction: column;
    gap: 24px;
    width: 357px;
    height: 314px;
    padding: 24px;
    border-radius: 16px;
    background: #FFF;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.10);
    transition: box-shadow 0.3s ease-in-out;
    cursor: pointer;

    &:hover {
        box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.20);
    }
}

.title {
    font-size: 24px;
    font-style: normal;
    font-weight: 700;
    line-height: 30px;
}

.info-block {
    display: flex;
    flex-direction: column;
    gap: 12px;
}

.info-block-row {
    display: flex;
    gap: 14px;
}

.info-block-text {
    font-size: 14px;
    font-style: normal;
    font-weight: 400;
    line-height: 20px;
}
</style>
