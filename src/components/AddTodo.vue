<template>
	<div>
		<form @submit="addTodo">
			<input type="text" name="title" placeholder="Add todo" v-model="title">
			<button type="submit" class="btn">Add</button>
		</form>
	</div>
</template>

<script>
	export default{
		name: "AddTodo",
		data() {
			return {
				title: '',
			}
		},
		methods: {
			addTodo(e) {
				// prevent form
				e.preventDefault();

				// create new todo
				const newTodo = {
					title: this.title,
					completed: false,
				};

				// send up to parent
				this.$emit('add-todo', newTodo);

				// clear title
				this.title = "";
			}
		}
	}
</script>

<style>
	form {
		display: flex;
	}
	form input {
		flex: 1;
		padding: 0.5rem;
	}
	.btn {
		border-color: #2980b9;
		background-color: #2980b9;
		color: #fff;
	}
</style>