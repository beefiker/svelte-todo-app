


<script lang="ts">

interface ITodoProps{
	work: string,
	done: boolean
}
	let name: string = 'Jaeyeong';

	let todoName = '';

	let todos:ITodoProps[] = [{
		work:'learn svelte',
		done: false
	}];

	const addTodos = (e) => {
		e.preventDefault();
		todos = [...todos, {work:todoName,done:false}]
		todoName = '';
	}
	const handleTodoChange = (e) => {
		todoName = e.target.value;
	}

	const handleTodos = (type : 'check' | 'remove', target:string) => {
		switch(type){
			case 'check':
			todos = todos.map((item:ITodoProps) => {
				if(item.work === target) item.done = !item.done
				return item;
			})
			break;
			case 'remove':
				console.log(`remove : ${target}`)
				todos = todos.filter((item:ITodoProps) => item.work !== target)
				break;
		}
	}

</script>

<main>
	<h1>Hello {name}!</h1>
	
	<form on:submit={addTodos}>
		<input type='text' value={todoName} on:change={handleTodoChange} placeholder="Add your todos" />
		<button on:click={addTodos}>Add</button>
	</form>

	<section class="user_todo">
		<ul class="todo_container">
			{#each todos as todo}
				<li>
					<span class={`${todo.done ? `done`:``}`}>{todo.work}</span> <span class={`${todo.done ? `check`:`none-check`}`} on:click={() => handleTodos('check', todo.work)}>V</span>
					<span class="delete_todo" on:click={() => handleTodos('remove', todo.work)}>X</span>
				</li>
			{/each}
		</ul>
	</section>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	.user_todo{
		max-width: 400px;
		height:100%;
		margin: 0 auto;
	}
	.todo_container{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		height:100%;
	}
	.delete_todo{
		color:red;
		font-weight: bold;
	}

	.done{
		text-decoration:line-through;
	}
	.none-check{
		color:gray;
		font-weight: bold;
	}
	.check{
		color:lime;
		font-weight: bold;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>