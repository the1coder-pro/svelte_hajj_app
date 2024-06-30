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
		Subnavbar,
		Searchbar,
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
		<Subnavbar inner={false}>
			<Searchbar searchContainer=".search-list" searchIn=".item-title" />
		</Subnavbar>
	</Navbar>

	<List strongIos outlineIos dividersIos class="searchbar-not-found">
		<ListItem title="Nothing found" />
	</List>
	<List strongIos outlineIos dividersIos class="search-list searchbar-found">
		{#each questions as question}
			<ListItem
				href="/teacher/{name}/{mainTitle}/{subTitle}/{question.Question}/"
				title={question.Question}
			/>
		{/each}
	</List>
</Page>
