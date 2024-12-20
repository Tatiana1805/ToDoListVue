<template>
    <form @submit.prevent="addTask">
        <!-- v-model="newTask" - двухстороняя связь -->
        <input v-model="newTask" type="text" placeholder="Напишите задачу" />
        <button type="submit">Добавить</button>
    </form>
    <TaskItem 
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @del-task="$emit('del-task', $event)"
        @toggle-task="$emit('toggle-task', $event)"
    />
    
</template>

<!-- setup - выполняется на этапе обработки -->
<script>
import { ref } from 'vue';
import TaskItem from './ToDoTask.vue'

export default {
    name: 'ToDoList',
    // берем данные из app
    emits: ['add-task-list', 'del-task', 'toggle-task'],
    props: ['tasks'],
    components: { TaskItem },

    // setup -функция жизненного цикла компонента
    setup(_, {emit}) {
        const newTask = ref('');

        const addTask = ()=>{
            if (newTask.value.trim()) {
                emit('add-task-list', newTask.value.trim())
                // при "добавить" очищается строка
                newTask.value = '';

            }
        }

        return { newTask, addTask }
    }
}

</script>

<!-- scoped - стили используются только в этом компоненте -->
<style>
    form {
        max-width: 70vw;
        display: flex;
    }

    input {
        height: 30px;
        border: none;
        border-radius: 5px;
        width: 40vw;
        margin-right: 20px;
    }

    button {
        padding: 10px 20px;
        background-color: #007bffb3;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    @media(max-width: 450px) {
        button{
            padding: 10px 5px;
        }
    }
</style>
