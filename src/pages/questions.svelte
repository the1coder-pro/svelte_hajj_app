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
	export let subTitle;
	export let mainTitle;
	export let name;

	// read all questions from data.json of the subTitle
	let questions = [];
	data.forEach((question) => {
		if (question.SubTitle === subTitle) {
			questions.push(question);
		}
	});
</script>

<Page name="questions">
	<Navbar>
		<NavTitle subtitle={mainTitle} style="font-size: 25px; padding: 20px;"
			>{subTitle}</NavTitle
		>
		<NavRight>
			<Button color="black" iconF7="arrow_right" back></Button>
		</NavRight>
	</Navbar>
	<Block>
		{#each questions as question}
			<Button
				href="/teacher/{name}/{mainTitle}/{subTitle}/{question.Question}/"
				large
				outline
				style="font-size: 15px; text-align: center; color:
					black;">{question.Question}</Button
			>
			<br />
		{/each}
	</Block>
</Page>
