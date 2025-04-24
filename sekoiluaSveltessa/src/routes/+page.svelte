<script lang="ts">
	const randomTaulukko: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
</script>

<h1>Otsikko</h1>

<button
	on:click={() => {
		const randomIndex = Math.floor(Math.random() * randomTaulukko.length);
		const randomElement = randomTaulukko[randomIndex];
		alert(randomElement);
	}}>Random numero 1-10</button
>
