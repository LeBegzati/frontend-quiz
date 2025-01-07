<script>
	import ListItem from '$lib/fonts/components/ListItem.svelte';
	let { data } = $props();
</script>

<h1>Welcome to the <strong class="text-primary">Leonit's Frontend Quiz!</strong></h1>
<p>Pick a subject to get started.</p>

<div class="flex flex-col gap-4">
	{#each data.quizzes as quiz, index (quiz.title)}
		<a href="/{quiz.title.toLowerCase()}"><ListItem title={quiz.title} icon={quiz.icon} /></a>
	{/each}
</div>
