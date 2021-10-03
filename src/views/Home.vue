<template>
    <AddTask v-show="showAddTask" @add-task="addTask"/>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="taskData"/>
</template>

<script>
    import AddTask from "@/components/AddTask";
    import Tasks from "@/components/Tasks";

    export default {
        name: "Home",
        props: {
            showAddTask: Boolean
        },
        components: {
            Tasks,
            AddTask,
        },
        data() {
            return {
                taskData: [],
            }
        },
        methods: {
            async addTask(task) {
                const res = await fetch('api/tasks', {
                    method: 'POST',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(task),
                })
                const data = await res.json()
                this.taskData = [...this.taskData, data]
            },
            async deleteTask(id) {
                if (confirm("Are you sure?")) {
                    const res = await fetch(`api/tasks/${id}`, {
                        method: 'DELETE',
                    })
                    res.status === 200
                        ? (this.taskData = this.taskData.filter((task) => task.id !== id))
                        : alert('Error deleting task')
                }
            },
            async toggleReminder(id) {
                const taskToToggle = await this.fetchTask(id)
                const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}
                const res = await fetch(`api/tasks/${id}`, {
                    method: 'PUT',
                    headers: {
                        'Content-type': 'application/json'
                    },
                    body: JSON.stringify(updateTask)
                })
                const data = await res.json()
                console.log('id toggle', id)
                this.taskData = this.taskData.map(task => task.id === id ? {...task, reminder: data.reminder} : task)
            },
            async fetchTasks() {
                const res = await fetch('api/tasks')
                return res.json();
            },
            async fetchTask(id) {
                const res = await fetch(`api/tasks/${id}`)
                return res.json();
            },
        }, async created() {
            this.taskData = await this.fetchTasks()
        }
    }
</script>

<style scoped>

</style>