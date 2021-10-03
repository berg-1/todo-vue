<template>
    <header>
        <h1>{{ title }}</h1>
        <Button :btnText="showAdd?'Close':'Add Task'" :color="showAdd?'red':'green'" v-show="homePage"
                @btn-click="$emit('toggle-add-task')"/>
    </header>
</template>

<script>
    import Button from "@/components/Button";

    export default {
        name: "Header",
        props: {
            title: {
                type: String,
                default: "Hello World"
            },
            showAdd: Boolean
        },
        components: {
            Button
        },
        computed: {
            homePage() {
                return this.$route.path === '/';
            }
        }
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>