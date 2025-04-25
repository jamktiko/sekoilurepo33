<!-- filepath: c:\sekoilurepo33\sekoiluaSveltessa\src\routes\+page.svelte -->
<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import kysymyksetData from '$lib/kysymykset.json';
	const randomTaulukko: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

	// Use the imported data directly
	let kysymykset: { kysymys: string; vastaus: string; vaara: string }[] = kysymyksetData;
	
	// Keep track of used questions
	let usedQuestionIndices: number[] = [];

	function getRandomWrongAnswers(correctAnswer: string, count: number = 2) {
			// Filter out the current correct answer to avoid duplicates
			const otherAnswers = kysymykset
					.filter(q => q.vastaus !== correctAnswer)
					.map(q => q.vastaus);
			
			// Alternative approach: pick random answers directly
			const result = [];
			const availableAnswers = [...otherAnswers]; // Copy to avoid modifying original
			
			for (let i = 0; i < count && availableAnswers.length > 0; i++) {
					const randomIndex = Math.floor(Math.random() * availableAnswers.length);
					result.push(availableAnswers[randomIndex]);
					// Remove to avoid duplicates
					availableAnswers.splice(randomIndex, 1);
			}
			
			return result;
	}
	
	function randomQuestion() {
			// Check if all questions have been used
			if (usedQuestionIndices.length >= kysymykset.length) {
					// Reset used questions if all questions have been shown
					usedQuestionIndices = [];
					alert("Kaikki kysymykset on käyty läpi. Aloitetaan alusta!");
			}
			
			// Add safety check to prevent errors if array is empty
			if (kysymykset.length === 0) {
					return { 
							kysymys: "Ei kysymyksiä saatavilla", 
							vastaus: "", 
							vaara: "",
							extraWrongAnswers: ["", ""]
					};
			}

			// Get a random index that hasn't been used yet
			let randomIndex: number;
			do {
					randomIndex = Math.floor(Math.random() * kysymykset.length);
			} while (usedQuestionIndices.includes(randomIndex) && usedQuestionIndices.length < kysymykset.length);
			
			// Track this question as used
			usedQuestionIndices.push(randomIndex);
			
			const kysymys = kysymykset[randomIndex];
			
			// Get two random wrong answers from other questions
			const extraWrongAnswers = getRandomWrongAnswers(kysymys.vastaus);
			
			return { ...kysymys, extraWrongAnswers };
	}

	// Initialize with the random question
	let randomKysymys = $state(randomQuestion());

	let vastaus = $derived(randomKysymys.vastaus);
	let vaara = $derived(randomKysymys.vaara);
	let extraWrongAnswers = $derived(randomKysymys.extraWrongAnswers || ["", ""]);

	function tarkistusVastaus(valinta: string) {
			if (valinta === randomKysymys.vastaus) {
					alert('Oikein!');
			} else {
					alert('Väärin!');
			}
	}
	
	// Add a function to get a new question
	function newQuestion() {
			randomKysymys = randomQuestion();
			vastaus = randomKysymys.vastaus;
			vaara = randomKysymys.vaara;
			extraWrongAnswers = randomKysymys.extraWrongAnswers || ["", ""];
	}

	// Alternative approach to shuffle answers without shuffleArray
	function randomizeAnswers() {
			const answers = [
					{ text: vastaus, isCorrect: true },
					{ text: vaara, isCorrect: false },
					{ text: extraWrongAnswers[0], isCorrect: false },
					{ text: extraWrongAnswers[1], isCorrect: false }
			];
			
			// Randomize the order by sorting with random comparison
			return answers.sort(() => Math.random() - 0.5);
	}

	let shuffledAnswers = $state(randomizeAnswers());

	// Re-randomize whenever we get a new question
	$effect(() => {
			if (randomKysymys) {
					shuffledAnswers = randomizeAnswers();
			}
	});
</script>

<h1>Otsikko</h1>

<Button
	onclick={() => {
			const randomIndex = Math.floor(Math.random() * randomTaulukko.length);
			const randomElement = randomTaulukko[randomIndex];
			alert(randomElement);
	}} 
	text="Random numero 1-10"
/>

<h1>{randomKysymys.kysymys}</h1>

<div>
	{#each shuffledAnswers as answer}
			<Button
					onclick={() => tarkistusVastaus(answer.text)}
					text={answer.text}
			/>
	{/each}
</div>

<!-- Added a button to get a new question -->
<Button onclick={() => newQuestion()} text="Uusi kysymys"/>