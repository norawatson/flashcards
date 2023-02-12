<script>

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Flashcards" />
</svelte:head>


<div class="card-container">
	<article class="question-card">
		What's 17 + 4?
	</article>
	<input placeholder="type answer here..."/>
</div>

<style>

	input {
		background: white;
	}

	.card-container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 60%;
		height: 100%;
		margin-left: auto;
		margin-right: auto;
	}

	.question-card {
		width: 100%;
	}
</style>