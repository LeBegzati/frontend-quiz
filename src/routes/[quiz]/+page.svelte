<script>
	import { page } from '$app/stores';
	let { data } = $props();
	let currentQuestion = $state(0);
</script>

{#each data.questions as question, index (question.question)}
	{#if index === currentQuestion}
		<p>Question {index + 1} of {data.questions.length}</p>
		<h2>{question.question}</h2>
	{/if}
{/each}

<button class="btn btn-primary" onclick={() => currentQuestion++}>Submit</button>
