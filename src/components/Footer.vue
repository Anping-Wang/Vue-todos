<template>
	<div class="footer">
		<span>Design By {{name}}</span>
	</div>
</template>

<script>
export default {
	data(){
		return {
			name : 'John'
		}
	}
}
</script>

<style lang = "less" scoped>
	.footer{
		margin-top: 40px;
	  	text-align: center;
	  	color: #bfbfbf;
	  	font-size: 10px;
	  	text-shadow: 0 1px 0 rgba(255, 255, 255, 0.5);
	}
</style>