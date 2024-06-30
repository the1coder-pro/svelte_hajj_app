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
	export let question;

	// get the question details from data.json
	let questions = [];
	data.forEach((quest) => {
		if (quest.Question === question) {
			questions.push(quest);
		}
	});
	console.log(questions.length);
</script>

<Page name="question">
	<Navbar>
		<NavTitle subtitle={mainTitle} style="font-size: 25px; padding: 20px;"
			>{subTitle}</NavTitle
		>
		<NavRight>
			<Button color="black" iconF7="arrow_right" back></Button>
		</NavRight>
	</Navbar>
	<Block>
		<h2 dir="rtl">{questions[0].Question}</h2>
		<p dir="rtl" style="font-size: 20px;">{questions[0].AnswerText}</p>
	</Block>
</Page>
