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
	export let mainTitle;
	export let name;

	// read all questions from data.json of the mainTitle
	let questions = [];
	console.log(mainTitle);
	data.forEach((question) => {
		if (question.MainTitle === mainTitle) {
			questions.push(question);
		}
	});

	let subTitles = [];

	// get only the mainTitle from the questions
	questions.forEach((question) => {
		if (!subTitles.includes(question.SubTitle)) {
			subTitles.push(question.SubTitle);
		}
	});
</script>

<Page name="subTitle">
	<Navbar>
		<NavTitle subtitle={name} style="font-size: 25px; padding: 20px;"
			>{mainTitle}</NavTitle
		>
		<NavRight>
			<Button color="black" iconF7="arrow_right" back></Button>
		</NavRight>
	</Navbar>
	<Block>
		<p class="grid grid-cols-2 grid-gap">
			{#each subTitles as title}
				<Button
					href="/teacher/{name}/{mainTitle}/{title}/"
					large
					outline
					style="font-size: 15px; padding: 60px; text-align: center; color:
							black;"
					><h3 style="text-wrap: pretty; line-height: 1.6;">
						{title}
					</h3>
				</Button>
			{/each}
		</p>
	</Block>
</Page>
