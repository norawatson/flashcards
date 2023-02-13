<script lang="ts">
	interface Flashcard {
		question: string;
		answer: string;
	}

	const cards: Flashcard[] = [
		{
			question: "Fill in the blanks to complete the definition.",
			answer: "This is what goes in the blanks."
		},
		{
			question: "What is the definition?",
			answer: "This is the definition."
		}
	];

	let currentIndex = 0;
	let showAnswer = false;

	function revealOrStep() {
		if (showAnswer) {
			if (currentIndex < cards.length - 1) {
				currentIndex = currentIndex + 1;
			}
			showAnswer = false;
		} else {
			showAnswer = true;
		}
	}

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Flashcards" />
</svelte:head>


<div class="card-container">
	<article class="question-card">
		{currentIndex + 1}.
		{cards[currentIndex][showAnswer ? "answer" : "question"]}
	</article>
	<button on:click={revealOrStep}>
		{showAnswer ? "Next" : "Show me!"}
	</button>
</div>

<style>
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