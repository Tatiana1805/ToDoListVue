<template>
    <!-- :class="{completed: task.completed} - переключение класса true на false -->
        <li :class="{completed: task.completed}">
            <span @click="$emit('toggle-task', task)">{{ task.text }}</span>
            <button @click="$emit('del-task', task.id)">Удалить</button>
        </li>
</template>

<script>
export default {
    name: 'TaskItem',
    props: ['task'],
    emits: ['del-task', 'toggle-task'],
}

</script>

<style scoped>
li {
    font-size: large;
    display: flex;
    justify-content: space-between;
    height: 37px;
    align-items: center;
    padding: 10px 0;
    cursor: pointer;
}

.completed {
    color: rgb(5, 255, 17);
}
</style>