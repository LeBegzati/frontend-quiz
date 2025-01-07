<script>
	let { icon, title, index, focusAction, incorrectAnswer, correctAnswer, disabled } = $props();
	let ABC = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
</script>

<button
	class="alert flex focus:outline focus:outline-primary {incorrectAnswer
		? 'outline outline-error'
		: ''} {correctAnswer ? 'outline outline-success' : ''}"
	onfocus={focusAction}
	{disabled}
>
	{#if icon}
		<img src={icon} alt={title + '-Icon'} />
	{:else}
		<span>{ABC[index]}</span>
	{/if}
	<span>{title}</span>
</button>
