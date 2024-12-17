<script>
	import { page } from '$app/stores';
	import { store } from '$lib/store.svelte.js';
	import ListItem from '$lib/components/ListItem.svelte';
	let { data } = $props();

	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

	let currentQuestion = $state(0);
	const progress = tweened(1, {
		duration: 400,
		easing: cubicOut
	});
	let selectedAnswer = $state('');
	let score = $state(0);
	let submitted = $state(false);

	function handleSubmit() {
		data.questions[currentQuestion].selectedAnswer = selectedAnswer;
		let solution = data.questions[currentQuestion].answer;
		if (selectedAnswer === solution) {
			score++;
		}
		submitted = true;
	}
	function nextQuestion() {
		submitted = false;
		selectedAnswer = '';
		currentQuestion++;
		$progress++;
	}
</script>

{#if currentQuestion < data.questions.length}
	{#each data.questions as question, index (question.question)}
		{#if index === currentQuestion}
			<p>Question {index + 1} of {data.questions.length}</p>
			<progress class="progress progress-primary w-56" value={$progress} max={data.questions.length}
			></progress>
			<h2>{question.question}</h2>

			{#each question.options as option, index (option)}
				{#key submitted}
					<ListItem
						title={option}
						{index}
						incorrectAnswer={question.selectedAnswer &&
							option === question.selectedAnswer &&
							question.selectedAnswer !== question.answer}
						focusAction={() => (selectedAnswer = option)}
						correctAnswer={question.selectedAnswer && option === question.answer}
						disabled={submitted}
					></ListItem>
				{/key}
			{/each}
		{/if}
	{/each}

	{#if !submitted}
		<button class="btn btn-primary" onclick={handleSubmit} disabled={!selectedAnswer}>Submit</button
		>
	{:else}
		<button class="btn btn-primary" onclick={nextQuestion}>Next Question</button>
	{/if}
{:else}
	<p>Game Over!</p>
	<p>You scored {score} out of {data.questions.length}!</p>
	<button class="btn btn-primary" onclick={window.location.reload()}>Play again!</button>
{/if}
