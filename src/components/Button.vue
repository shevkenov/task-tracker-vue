<template>
    <button :style="{background: color}" @click="showForm" class="btn">{{text}}</button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        color: String,
    },
    methods: {
        showForm() {
            this.$emit('show-form');
        }
    }
}
</script>