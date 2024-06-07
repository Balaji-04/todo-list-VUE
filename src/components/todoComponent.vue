<script setup lang="ts">
    import {ref} from 'vue';
    interface Task {
        id: Number,
        taskName: String,
        status: boolean
    }
    let taskId = 0;
    let currTaskName: String = "";
    const tasks = ref<Task[]>([]);

    function addTask(){
        if (currTaskName !== ""){
            const currTask: Task = {
                id: taskId,
                taskName: currTaskName,
                status: false
            };
            taskId++;
            tasks.value.push(currTask);
        }else{
            document.querySelector('.msg').innerHTML = 'please enter a taskName!';
            setTimeout(() => {
                document.querySelector('.msg').innerHTML = '';
            }, 6000);
        }
    }

    function completed(CtaskId: number){
        const toBeDeleted = tasks.value.findIndex((ele) => {
            return ele === tasks.value[CtaskId];
        });
        tasks.value.splice(toBeDeleted , 1);
    }

    defineProps();
</script>

<template>
    <h1>To-do List</h1>
    <input v-model="currTaskName" />
    <button @click="addTask()">Add Task</button>
    <div class="allTasks">
        <table>
            <tr v-for="t in tasks">
                <!-- <td>{{ t.id }}</td> -->
                <td>{{ t.taskName }}</td>
                <td><button @click="completed(t.id)">&#10005;</button></td>
            </tr>
        </table>
    </div>
    <div class="msg"></div>
</template>