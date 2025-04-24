<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	const randomTaulukko: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

		let kysymykset = [
			{
				kysymys: 'Mikä on pääkaupunki Suomessa?',
				vastaus: 'Helsinki',
				vaara: 'Tampere'
			},
			{
				kysymys: 'Mikä on Suomen kansalliskukka?',
				vastaus: 'Suomenruusu',
				vaara: 'Kielo'
			},
			{
				kysymys: 'Mikä on Suomen kansallislintu?',
				vastaus: 'Laulujoutsen',
				vaara: 'Koskikara'
			},
			{
				kysymys: 'Mikä on Suomen kansallispeli?',
				vastaus: 'Pesäpallo',
				vaara: 'Jalkapallo'
			},
			{
				kysymys: 'Mikä on Suomen kansallisruoka?',
				vastaus: 'Karjalanpiirakka',
				vaara: 'Karjalanpaisti'
			},
			{
				kysymys: 'Mikä on Suomen kansallislaulu?',
				vastaus: 'Maamme-laulu',
				vaara: 'Finlandia-hymni'
			},
			{
				kysymys: 'Mikä on Suomen kansalliskala?',
				vastaus: 'Siika',
				vaara: 'Ahven'
			},
			{
				kysymys: 'Mikä on Suomen kansallispuu?',
				vastaus: 'Tervaleppä',
				vaara: 'Mänty'
			},
			{
				kysymys: 'Mikä on Suomen kansallisväri?',
				vastaus: 'Sininen ja valkoinen',
				vaara: 'Punainen ja valkoinen'
			},
			{
				kysymys: 'Mikä on Suomen kansalliseläin?',
				vastaus: 'Karhu',
				vaara: 'Susi'
			}];

			function randomQuestion() {
				const randomIndex = Math.floor(Math.random() * kysymykset.length);
				const kysymys = kysymykset[randomIndex];
				return kysymys
			}


			let randomKysymys = randomQuestion();

			let vastaus = $state(randomKysymys.vastaus);
			let vaara = $state(randomKysymys.vaara);

			function tarkistusVastaus(valinta: string) {
				if (valinta === randomKysymys.vastaus) {
					alert('Oikein!');
				} else {
					alert('Väärin!');
				}
			}
</script>

<!-- <h1>Otsikko</h1>

<Button
	onclick={() => {
		const randomIndex = Math.floor(Math.random() * randomTaulukko.length);
		const randomElement = randomTaulukko[randomIndex];
		alert(randomElement);}} text="Random numero 1-10"/> -->



<h1> {randomKysymys.kysymys}</h1>

<div>

	<Button
		onclick={() => tarkistusVastaus(randomKysymys.vastaus)}
		text={vastaus}/>
		<Button
		onclick={() => tarkistusVastaus(randomKysymys.vaara)}
		text={vaara}/>
</div>



