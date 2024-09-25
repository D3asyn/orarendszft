<script>
	import { onMount } from "svelte";
	import orarend from "../public/orarend.json";

	console.log(orarend);

	function extractClassesByDay(data) {
		const classesByDay = {};

		data.forEach((entry) => {
			const day = entry.nap;
			const classInfo = {
				target: entry.targy,
				teacher: entry.tanar,
				classroom: entry.terem,
				period: entry.ora,
			};

			// Initialize the day's entry if it doesn't exist
			if (!classesByDay[day]) {
				classesByDay[day] = [];
			}

			// Add the class info to the day's entry
			classesByDay[day].push(classInfo);
		});

		return classesByDay; // Return the object containing classes grouped by day
	}

	// Get classes grouped by day
	const classesByDay = extractClassesByDay(orarend);
</script>

<main>
	<h1>Classes Scheduled by Day</h1>
	{#each Object.entries(classesByDay) as [day, classes]}
		<div class="day">
			<h2>{day}</h2>
			<ul>
				{#each classes as classs}
					<li>
						{classs.target} (Period: {classs.period}, Room: {classs.classroom})
					</li>
				{/each}
			</ul>
		</div>
	{/each}
</main>
