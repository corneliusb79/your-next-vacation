<script type="ts">
	import { Button, Card, Heading, P } from 'flowbite-svelte';
	import Questions from '../components/Questions.svelte';

	let answers: Record<string, number> = {
		beaches: 1,
		warmWeather: 1,
		rain: 1,
		casino: 1
	};

	interface Place {
		name: string;
		attributes: Record<string, number>;
		funFact: string;
		image: string;
	}

	const places: Array<Place> = [
		{
			name: 'California',
			attributes: {
				beaches: 3,
				warmWeather: 4
			}
		},
		{
			name: 'Alaska',
			attributes: {
				beaches: 3,
				warmWeather: 0
			}
		},
		{
			name: 'London',
			attributes: {
				beaches: 1,
				warmWeather: 2,
				rain: 5
			}
		},
		{
			name: 'Mumbai',
			attributes: {
				beaches: 1,
				warmWeather: 5,
				rain: 2
			}
		},
	];

	let placesWithScore: Array<{ place: Place; score: number }> = [];

	$: {
		let pws = [];
		for (const place of places) {
			let score = 0;
			if (place.name === "London" && answers.rain === 5) {
				score += 10000000000
			}
			for (const answerKey of Object.keys(answers)) {
				if (answerKey in place.attributes) {
					score += place.attributes[answerKey] * answers[answerKey];
				}
			}
			pws.push({ place, score });
		}
		placesWithScore = pws.sort((a, b) => (a.score === b.score ? 0 : a.score < b.score ? 1 : -1));
	}

	let recommendedPlace: Place | null = null

	function submit(){
		recommendedPlace = placesWithScore[0].place;
	}
</script>

<div class="p-4">
	<Heading tag="h1" class="mb-4" customSize="text-4xl font-extrabold  md:text-5xl lg:text-6xl">
		Your next Vacation
	</Heading>

	<div class="p-4 max-w-[750px] gap-4 flex flex-col">
		<Questions
			question="How much do you like beaches?"
			on:change={(event) => {
				answers = { ...answers, beaches: event.detail };
			}}
			score={answers.beaches}
		/>
		<Questions
			question="How much do you like warm weather?"
			on:change={(event) => {
				answers = { ...answers, warmWeather: event.detail };
			}}
			score={answers.warmWeather}
		/>
		<Questions
			question="How much do you enjoy rain?"
			on:change={(event) => {
				answers = { ...answers, rain: event.detail };
			}}
			score={answers.rain}
		/>
		<Questions
		question="How much do you enjoy going to the casino?"
		on:change={(event) => {
			answers = { ...answers, casino: event.detail };
		}}
		score={answers.casino}
		/>
		<Button color="purple" on:click={submit}>Submit</Button>
	</div>

	{#if recommendedPlace !== null}
		<Card>
			<div class="flex flex-col gap-2">
				<Heading tag="h4">{recommendedPlace.name}</Heading>
				<img src={recommendedPlace.image} alt={recommendedPlace.name} />
				<P color="text-gray-700">{recommendedPlace.funFact}</P>
			</div>
		</Card>
	{/if}
</div>

