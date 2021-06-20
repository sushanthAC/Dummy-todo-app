<template>
    <div :class="[todo.completed ? 'bgColor-completed':'bgColor-pending', 'todo']">
        <h3 class="todoHead">{{todo.title}}</h3>
        <h4 class="todoFooter" v-if="!todo.completed"><button @click="$emit('markAsCompleted', todo)">Mark as completed</button> </h4>
        <h4 class="todoFooter" v-if="todo.completed">Completed</h4>
    </div>
</template>

<script>
    export default {
        name: "Task",
        props:['todo']
    }
</script>

<style scoped>
.bgColor-completed {
    background: #056534;
}
.bgColor-pending {
    background: #10da73;
}
.todo {
    border-radius: 5px;
    padding: 0 10px;
    border: 2px solid black;
    align-self: flex-start;
}
button {
    height: 30px;
    background: cadetblue;
    border-radius:5px ;
    cursor: pointer;
}
</style>