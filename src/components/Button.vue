<template>
    <button @click="onClick()" :style="{background: color}" class="btn">{{ btnText }}d</button>
</template>

<script>
    export default {
        name: "Button",
        props: {
            color: String,
            btnText: String,
            showAdd: Boolean
        },
        methods: {
            onClick() {
                this.$emit('btn-click')
            }
        }
    }
</script>

<style scoped>

</style>