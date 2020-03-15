<script>
	import { onMount } from 'svelte';

	let username = '';
	const tdna = new TypingDNA();

	const submit = async (event) => {
		event.preventDefault();

		const dna = tdna.getTypingPattern({ type: 2, text: username });

		try {
			await fetch(`http://localhost:8080/save/${username}`, {
				method: 'POST',
				body: JSON.stringify({
					tp: dna,
				})
			})

			alert('signup with success');
		} catch (error) {
			console.log(error);
		}
	}
</script>

<main>
	<div>
		<h3>To signup, type your username  </h3>
		<form on:submit={submit}>
			<input
				type="text"
				bind:value={username}
			/>
			<button type="submit"> Signup </button>
		</form>
	</div>
</main>
