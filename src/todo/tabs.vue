<template>
<div class="helper">
    <span class="left">{{ unfinishedTodoLength}}items left</span>
    <span class="tabs">
        <span v-for="state in states"
               :key="state"
              :class="[state, filter === state ? 'actived' : '']"
              @click="toggleFilter(state)"
        >{{state}}
        </span>
    </span>
    <span class="clear" @click="clearALLComponents">clear commpleted</span>
</div>
</template>
<script>
    export default {
        props:{
            filter:{
                type:String,
                required:true
            },
            todos:{
                type:Object,
                required:true
            }
        },
        data(){
            return{
                states:['all','active','completed']
            }
        },
        computed:{
          unfinishedTodoLength(){
            return this.todos.filter(todo=>!todo.completed).length;
          }
        },
        methods:{
            clearALLComponents(){
                this.$emit('clearALLComponents')
            },
            toggleFilter(state){
           this.$emit('toggle',state);
            }
        }
    }
</script>
<style type="text/stylus" lang="stylus" scoped>
.helper{
    width  100%
    background-color #fff
    display flex
    justify-content space-between
    padding  5px 0
    box-sizing border-box
    line-height:30px
    font-smoothing: antialiased
}
.left,.tabs,.clear{
    padding  0 10px
    box-sizing border-box
}
    .left,.clear {
        width 150px
    }
    .left{
        text-align left
    }
    .clear{
        text-align right
        cursor pointer
    }
    .tabs{
        width 200px
        display flex
        justify-content space-around
        *{
            display inline-block
            padding 0 5px
            cursor pointer
            &.actived{
                border:solid 1px #ccc
                border-radius 5px
            }
        }

    }

</style>