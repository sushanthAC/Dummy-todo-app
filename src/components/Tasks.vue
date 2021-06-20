<template>
    <div class="main">
        <span class="heading">Task List</span>
        <div class="search">
            <input class="inp" type="text" v-model="todoTask" />&nbsp;&nbsp;
            <button @click="addNewTask">Add New Task</button>
        </div>
        <div class="show">
            <h4 class="showLabel">Show only &nbsp;</h4>
            <select class="showSelect" v-model="noOfItems" @change="getLimitedTodos">
                <option value="">All</option>
                <option value="100">100</option>
                <option value="50">50</option>
                <option value="25">25</option>
                <option value="10">10</option>
                <option value="5">5</option>
            </select>
        </div>
        <div class="search">
            <input class="seachBox" type="text" placeholder="Search Todo Task" @keyup="filterTodo" v-model="filter"/>
        </div>
        <div class="todosList">
           <template v-for="todo in todoList" :key="todo.id">
               <Task :todo="todo" @markAsCompleted="$emit('markAsCompleted', todo.id)"/>
           </template>
        </div>
        <span class="footer">Task List footer</span>
    </div>
</template>

<script>
    import Task from './Task.vue';
    export default {
        name: "Tasks",
        props:['todoList'],
        data() {
            return {
                noOfItems:"",
                filter:"",
                todoTask:""
            }
        },
        methods:{
            getLimitedTodos() {
                console.log('logggg');
                this.$emit('getLimitedTodos', this.noOfItems);
            },
            filterTodo() {
                this.$emit('filterTodo', this.filter);
            },
            addNewTask() {
                let newTask = {
                    id:Math.floor(Math.random() * 10000),
                    title: this.todoTask,
                    userId: 1,
                    completed: false
                }
                this.$emit('addNewTask', newTask);
            }
        },
        components:{
            Task
        }       
    }
   
</script>

<style scoped>
.footer {
    margin: 50px 0;
}
.todosList {
    display:flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
    flex: 1;
}

.main{
    text-align: center;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    font-weight: 700;
    display: flex;
    flex-direction: column;
    height: 712px;
}

.heading {
    font-size: 30px;     
}

.search {
    display: flex;
    justify-content: center;
    height: 35px;
    margin: 2% 20%;    
}

input, button {    
    border-radius: 5px; 
}

input{
    flex:2;
    height: 30px;
    background: #bdd6be;
}

button {
    flex:1;
    cursor: pointer;
    background: #10da73;
}

.show{
    display: flex;
    justify-content: center;
    align-items: center;    
}
.showSelect{
    height: 30px;
    border-radius: 5px; 
    flex-basis: 60px;
}
.seachBox{
    flex-grow: 0;
    height: 30px;
}

@media only screen and (max-width: 500px) {
    .todosList {
        display:flex;
        align-items: center;
        flex-wrap: wrap;    
    }
    .todo {
        margin: 3% 0;
    }
    .main{
        height: 0;
    }
}

</style>