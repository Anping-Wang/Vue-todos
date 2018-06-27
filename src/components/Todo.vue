<template>
	<div :class = "['todo',todo.completed === true ? 'completed' : '']">
		<input type = "checkbox" class = "toggle" v-model = "todo.completed">
		<span>{{todo.content}}</span>
		<button class="destroy" @click = "deleateTodo"></button>
	</div>
</template>

<script>
export default {
	props: {
		//接收父组件传来的数据
		todo: {
			type: Object,
			required: true
		}
	},
	methods: {
		deleateTodo(){
			this.$emit('del',this.todo.id)
		}
	},
	computed: {

	}
}
</script>

<style lang="less" scoped>
	.todo {
        position: relative;
        background-color: #fff;
        font-size: 24px;
        border-bottom: 1px solid rgba(0,0,0,0.06);
        &:hover {
            .destroy:after{
                content: '×'
            }
        }
        span {
            white-space: pre-line;
            word-break: break-all;
            padding: 15px 60px 15px 15px;
            margin-left: 45px;
            display: block;
            line-height: 1.2;
            transition: color 0.4s;
        }
        &.completed{
            span {
                color: #d9d9d9;
                text-decoration: line-through
            }
        }
    }
    .toggle{
        text-align: center;
        width: 40px;
        height: 40px;
        line-height: 40px;
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto 0;
        border: none;
        appearance: none;       /*隐藏单选按钮*/
        outline: none;          /*点击单选按钮时，不显示外边线*/
        padding-left: 10px;
        cursor: pointer;
 		&:after{
            content: url('../../static/image/round.svg')
        }
        &:checked:after{
            content: url('../../static/image/done.svg')
        }
    }
    .destroy {
        position: absolute;
        top: 0;
        right: 10px;
        bottom: 0;
        width: 40px;
        height: 40px;
        margin: auto 0;
        font-size: 30px;
        color: #cc9a9a;
        margin-bottom: 11px;
        transition: color 0.2s ease-out;
        background-color: transparent;
        appearance: none;
        border-width: 0;
        cursor: pointer;
        outline: none
    }
</style>