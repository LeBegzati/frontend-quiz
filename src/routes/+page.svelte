<script>
	import ListItem from '$lib/fonts/components/ListItem.svelte';
	export let data;
</script>

<h1>Welcome to the <strong class="text-primary">Frontend Quiz!</strong></h1>
<p>Pick a subject to get started</p>

<div class="flex flex-col gap-4">
	{#each data.quizzes as quiz, index (quiz.title)}
		<a href="/{quiz.title.toLowerCase()}"><ListItem title={quiz.title} {index} /></a>
	{/each}
</div>

<!-- Open the modal using ID.showModal() method  <button class="btn" onclick="my_modal_1.showModal()">...and DaisyUI (click)</button>
<dialog id="my_modal_1" class="modal">
	<div class="modal-box">
		<h3 class="text-lg font-bold">Hello from Daisy 🌻!</h3>
		<p class="py-4">Press ESC key or click the button below to close</p>
		<div class="modal-action">
			<form method="dialog">
				 if there is a button in form, it will close the modal 
				<button class="btn">Close</button>
			</form>
		</div>
	</div>
</dialog> -->
