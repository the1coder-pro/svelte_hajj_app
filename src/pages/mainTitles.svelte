<script>
	import {
		Page,
		Navbar,
		List,
		ListInput,
		ListItem,
		Toggle,
		BlockTitle,
		Button,
		Range,
		NavRight,
		Block,
		NavTitle,
	} from "framework7-svelte";

	import data from "./data.json";
	export let name;

	// read all questions from data.json
	let questions = [];
	data.forEach((question) => {
		questions.push(question);
	});

	let mainTitles = [];

	// get only the mainTitle from the questions
	questions.forEach((question) => {
		if (!mainTitles.includes(question.MainTitle)) {
			mainTitles.push(question.MainTitle);
		}
	});
</script>

<Page name="teacher">
	<Navbar>
		<NavTitle style="font-size: 25px; padding: 20px;">{name}</NavTitle>
		<NavRight>
			<Button color="black" iconF7="arrow_right" back></Button>
		</NavRight>
	</Navbar>
	<Block>
		<p class="grid grid-cols-2 grid-gap">
			{#each mainTitles as title}
				<Button
					href="/teacher/{name}/{title}/"
					large
					outline
					style="font-size: 15px; padding: 60px; text-align: center; color:
							black;"
					><h3>
						{title}
					</h3>
				</Button>
			{/each}
		</p>
	</Block>
</Page>
