<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	const randomTaulukko: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
</script>

<h1>Otsikko</h1>

<Button
	onclick={() => {
		const randomIndex = Math.floor(Math.random() * randomTaulukko.length);
		const randomElement = randomTaulukko[randomIndex];
		alert(randomElement);}} text="Random numero 1-10"/>
<h1>Welcome to SvelteKit</h1>
<p>
	Lorem ipsum dolor sit amet consectetur adipisicing elit. Facilis a ut fuga nihil necessitatibus
	unde illum ab consectetur? Voluptatibus similique asperiores labore enim necessitatibus maiores
	ipsum debitis nihil cum cupiditate.
</p>
<p>Visit <a href="https://svelte.dev">svelte.dev</a> to learn how to build Svelte apps.</p>
