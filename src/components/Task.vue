<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
        <h3>{{ task.text }}
            <i class="far fa-circle" @click="$emit('delete-task')"></i>
        </h3>
        <p>{{ task.day }}</p>
    </div>
</template>

<script>
    export default {
        name: "Task",
        props: {
            task: Object
        },
        methods: {
        }
    }
</script>

<style scope>
    .far {
        color: grey;
    }

    .task {
        background: #f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
    }

    .task.reminder {
        border-left: 5px solid green;
    }

    .task h3 {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>