<script lang="ts">
	import Markdown from "$lib/Markdown.svelte";

	interface Flashcard {
		question: string;
		answer: string;
	}

	const cards: Flashcard[] = [
		{
			question: `Evaluate the following integral.

$$
\\int_0^π \\sin x \\mathrm{d}x
$$`,
			answer: "$$\n2\n$$"
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
			} else {
				currentIndex = 0;
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
	<Markdown
		defaultValue={cards[currentIndex][showAnswer ? "answer" : "question"]}
		readonly/>
	<button on:click={revealOrStep}>
		{showAnswer ? "Next" : "Show me!"}
	</button>
</div>

<style>
	.card-container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: stretch;
		gap: 1rem;
		width: 60%;
		height: 100%;
		margin-left: auto;
		margin-right: auto;
		margin-top: 4rem;
	}
</style>