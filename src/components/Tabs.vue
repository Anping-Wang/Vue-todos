<template>
	<div class="tabs">
		<span class="left">
			{{unCompletedTodos}} items left
		</span>
		<span class = "center">
			<span 
				:class="filter === state ? 'actived' : ''"
				v-for ="state in states"
				@click = "toggleFilter(state)"
			>
			{{state}}
			</span>
		</span>
		<span class="clear">
			<span @click = "clearAll" class="all">clear all</span>
			<b>|</b>
			<span class = "completed" @click = "clearCompleted">clear completed</span>
		</span>
		
	</div>
</template>

<script>
export default {
	props: {
		todos: {
			type: Array,
			required: true
		},
		filter: {
			type: String,
			required: true
		}
	},
	data(){
		return{
			states: ['all','active','complete']
		}
	},
	methods: {
		toggleFilter(state){
			this.$emit('toggleFilter',state)
		},
		clearAll(){
			this.$emit('clearAll')
		},
		clearCompleted(){
			this.$emit('clearCompleted')
		}
	},
	computed: {
		unCompletedTodos(){
			return this.todos.filter(todo => todo.completed === false).length
			// return this.todos.filter(todo => !todo.completed).length
		}
	}	
}
</script>

<style lang="less" scoped>
	.tabs {
        font-weight: 100;
        display: flex;
        justify-content: space-between;
        padding: 5px 0;
        line-height: 30px;
        background-color: #ffffff;
        font-size: 14px;
        font-smoothing: antialiased;

        .left, .clear, .center {
        	padding: 0 10px;
        	box-sizing: border-box
    	}

    	.left {
       	 	width: 150px;
			text-align: left
    	}

    	.clear {
    		display: flex;
        	text-align: right;
        	cursor: pointer;
        	.all {
        		padding-right: 10px;
        	}
        	.completed {
        		padding-left: 10px
        	}
        	b{
        		color: #ccc;
        	}
    	};

    	.center {
	        width: 200px;
	        display: flex;
	        justify-content: space-around;
	        * {
	            display: inline-block;
	            padding: 0 10px;
	            cursor: pointer;
	            border: 1px solid rgba(175, 47, 47, 0);
	            &.actived {
	                border-color: rgba(175, 47, 47, 0.4);
	                border-radius: 5px
	            }
	        }
    	}
    }   
</style>