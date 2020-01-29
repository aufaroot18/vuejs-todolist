<template>
	<div class="todo-item" v-bind:class="{ 'is-complete': todo.completed }">
		<p>
			<input type="checkbox" v-on:change="markComplete" v-bind:checked="todo.completed">
			{{ todo.title }}
			<button class="del" v-on:click="$emit('del-todo', todo.id)">X</button>
		</p>
	</div>
</template>

<script>
	export default{
		name: "Todoitem",
		props: ["todo"],
		methods: {
			markComplete() {
				this.todo.completed = !this.todo.completed;
			}
		}
	}
</script>

<style scope>
	.todo-item {
		padding: 1rem;
		background-color: #f4f4f4;
		border-bottom: 1px solid #ccc;
	}

	.is-complete {
		text-decoration: line-through;
	}

	.del {
		background-color: #e74c3c;
		border-color: #e74c3c;
		float: right;
	}
</style>