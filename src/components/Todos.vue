<template>
	<div class = "todos">
		<!-- <input type="checkbox" v-model="turn">  
		v-model绑定checkbox可以控制其是否被选中-->
		<input type = "text"
			placeholder = '接下来要做什么？'
			class = 'input-box'
			autofocus = true
			@keyup.enter = 'addTodo'
			v-model='msg'
		>
		<Todo 
			:todo = 'todo'
			v-for = "todo in filteredTodos"
			:key = "todo.id"
			@del = "deleteTodo"
		/>
		<Tabs
			:todos = "todos"
			@toggleFilter = "toggle"
			:filter = 'filter'
			@clearAll = "clearAll"
			@clearCompleted = "clearCompleted"
		/>
	</div>
</template>

<script>
import Todo from './Todo.vue'
import Tabs from './Tabs.vue'

let id = 0; 
export default {
	data(){
		return {
			msg: '',
			todos: [],
			filter: 'all',
			// turn: false
		}
	},
	methods: {
		addTodo(e){
			//方法一:
			// if(e.target.value.trim()){
			// 	this.todos.unshift({
			// 		id: id++,
			// 		content: e.target.value.trim(),
			// 		completed: false
			// 	});
			// 	e.target.value = ''

			// }else{
			// 	alert('逗我玩呢，啥也不写？？？')
			// }

			//方法二:
			if(this.msg.trim()){
				this.todos.unshift({
					id: id++,
					content: this.msg,
					completed: false
				})
			}else{
				alert('逗我玩呢，啥也不写？？？')
			};
			this.msg=''
		},
		deleteTodo(id){
			this.todos.splice(this.todos.findIndex(todo => todo.id === id),1)
		},
		toggle(state){
			this.filter = state
		},
		clearAll(){
			this.todos = []
		},
		clearCompleted(){
			this.todos = this.todos.filter(todo => todo.completed === false)
		}
	},
	computed: {
		filteredTodos(){
			if(this.filter === 'all'){
				return this.todos
			}else if(this.filter === 'active'){
				return this.todos.filter(todo => todo.completed === false)
			}else{
				return this.todos.filter(todo => todo.completed === true)
			};

		}
	},
	components: {
		Todo,
		Tabs,
	}
}
</script>

<style lang = 'less' scoped>
	.todos {
        width: 600px;
        margin: 0 auto;
        box-shadow: 0 0 5px #666;
    }

    .input-box {
        position: relative;
        margin: 0;
        width: 100%;
        font-size: 24px;
        font-family: inherit;
        font-weight: inherit;
        line-height: 1.4em;
        border: 0;
        outline: none;
        color: inherit;
        box-sizing: border-box;
        font-smoothing: antialiased;
        padding: 16px 16px 16px 36px;
        border: none;
        box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
    }
</style>