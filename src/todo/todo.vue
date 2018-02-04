<template>
    <section class="real-app">
        <input type="text"
               class="add-input"
               placeholder="接下来要做什么?"
               @keyup.enter="addTodo"
               autofocus="autofocus"
        />
        <Item :todo="todo"
              v-for="todo in filteredTodos "
              :key=todo.id
              @del="deleteTodo "
        >
        </Item>
        <Tabs :filter="filter"
               @toggle="toggleFilter"
              @clearALLComponents="clearALLComponents"
              :todos="todos"
        ></Tabs>
    </section>
</template>

<script>
    import Item from './item.vue'
    import Tabs from './tabs.vue'
    let id=0;
    export default {
        data(){
            return {
                todos : [],
                filter: 'all'
            }
        },
        components:{
            Item,
            Tabs
        },
        computed:{
            filteredTodos (){
                if(this.filter==='all'){
                    return this.todos
                }
                const completed=this.filter==='completed';
               return this.todos.filter(todo => completed === todo.completed)
            }
        },
        methods:{
            addTodo(e){
                this.todos.unshift({
                    id:id++,
                    content:e.target.value.trim(),
                    completed:false
                })
                e.target.value=""
            },
            deleteTodo(id){
                this.todos.splice(this.todos.findIndex(todo => todo.id === id),1);
            },
            toggleFilter(state){
                this.filter=state
            },
            clearALLComponents(){
                this.todos=this.todos.filter(todo=>!todo.completed);
            }
        }
    }
</script>

<style lang="stylus" scoped>
    .real-app{
        width: 500px;
        margin: 0 auto;
        box-shadow 0 0 5px #666
    }
    .add-input{
        width: 100%;
        height: 50px;
        font-size: 24px;
        outline: none;
        padding-left:50px ;
        font-family: inherit;
        font-weight: inherit;
        border: solid 1px #999;
        box-sizing: border-box;
        border none
        box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
    }
</style>
