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
		Card,
		CardFooter,
		CardHeader,
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
			<Searchbar
				placeholder="البحث"
				searchContainer=".search-list"
				searchIn=".item-title"
			/>
		</Subnavbar>
	</Navbar>

	<List strongIos outlineIos dividersIos class="searchbar-not-found">
		<ListItem title="لا توجد أسئلة" />
	</List>
	<List
		dir="rtl"
		dividersIos
		mediaList
		outlineIos
		strongIos
		class="search-list searchbar-found"
	>
		{#each questions as question}
			<ListItem
				link="/teacher/{name}/{mainTitle}/{subTitle}/{question.Question}/"
				title={question.Question}
			/>
		{/each}
	</List>
</Page>

<!-- <ListItem

link="/teacher/{name}/{mainTitle}/{subTitle}/{question.Question}/"
title={question.Question}
subtitle={mainTitle}
/> -->
