<script>
	import {
		Page,
		Navbar,
		NavTitle,
		NavRight,
		Link,
		Toolbar,
		Block,
		List,
		ListItem,
		Button,
		Subnavbar,
		Searchbar,
		Tabs,
		Tab,
		Fab,
		Icon,
		Popup,
	} from "framework7-svelte";

	let teachers = [
		"شيخ علي العبدالكريم",
		"شيخ حسين السعيد",
		"شيخ حسن المطوع",
		"شيخ أحمد المطوع",
		"شيخ عبدالله العبدالله",
		"سيد زكريا الحاجي",
		"سيد عبدالله الحاجي",
		"شيخ علي الدهنين",
	];

	let popupOpened = false;

	// get questions from data.json
	let questions = [];
	import data from "./data.json";
	data.forEach((question) => {
		questions.push(question);
	});
</script>

<Page name="home" pageContent={false}>
	<!-- Top Navbar -->

	<Navbar>
		<NavTitle style="font-size: 25px; padding: 20px;">حج التمتع</NavTitle>
	</Navbar>

	<Toolbar topMd tabbar>
		<Link tabLink="#tab-1" tabLinkActive style="font-size: 20px;">المعلمين</Link
		>
		<Link tabLink="#tab-2" style="font-size: 20px;">الإعلانات</Link>
	</Toolbar>
	<Tabs>
		<Tab id="tab-1" class="page-content" tabActive>
			<Block>
				<p class="grid grid-cols-2 grid-gap">
					{#each teachers as teacher}
						<Button
							href="/teacher/{teacher}/"
							large
							outline
							style="font-size: 15px; text-align: center; color:
							black;">{teacher}</Button
						>
					{/each}
				</p>
			</Block>
			<Fab position="right-bottom" onClick={() => (popupOpened = !popupOpened)}>
				<Icon md="material:search" />
			</Fab>
			<Popup
				class="demo-popup-swipe"
				swipeToClose
				onPopupClosed={() => (popupOpened = false)}
				opened={popupOpened}
			>
				<Page>
					<Navbar title="البحث">
						<Searchbar searchContainer=".search-list" searchIn=".item-title" />
						<NavRight>
							<Button color="black" iconF7="arrow_right" popupClose></Button>
						</NavRight>
					</Navbar>
					<List strongIos outlineIos dividersIos class="searchbar-not-found">
						<ListItem title="لا توجد أسئلة بمثل ما كتبت" />
					</List>
					<List
						strongIos
						outlineIos
						dividersIos
						class="search-list searchbar-found"
					>
						{#each questions as question}
							<ListItem dir="rtl" title={question.Question} />
						{/each}
					</List>
				</Page>
			</Popup>
		</Tab>

		<Tab id="tab-2" class="page-content">
			<Block>
				<p>Tab 2 content</p>
				<p>
					Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ullam enim
					quia molestiae facilis laudantium voluptates obcaecati officia cum,
					sit libero commodi. Ratione illo suscipit temporibus sequi iure ad
					laboriosam accusamus?
				</p>
				<p>
					Saepe explicabo voluptas ducimus provident, doloremque quo totam
					molestias! Suscipit blanditiis eaque exercitationem praesentium
					reprehenderit, fuga accusamus possimus sed, sint facilis ratione quod,
					qui dignissimos voluptas! Aliquam rerum consequuntur deleniti.
				</p>
				<p>
					Totam reprehenderit amet commodi ipsum nam provident doloremque
					possimus odio itaque, est animi culpa modi consequatur reiciendis
					corporis libero laudantium sed eveniet unde delectus a maiores nihil
					dolores? Natus, perferendis.
				</p>
				<p>
					Atque quis totam repellendus omnis alias magnam corrupti, possimus
					aspernatur perspiciatis quae provident consequatur minima doloremque
					blanditiis nihil maxime ducimus earum autem. Magni animi blanditiis
					similique iusto, repellat sed quisquam!
				</p>
				<p>
					Suscipit, facere quasi atque totam. Repudiandae facilis at optio
					atque, rem nam, natus ratione cum enim voluptatem suscipit veniam!
					Repellat, est debitis. Modi nam mollitia explicabo, unde aliquid
					impedit! Adipisci!
				</p>
				<p>
					Deserunt adipisci tempora asperiores, quo, nisi ex delectus vitae
					consectetur iste fugiat iusto dolorem autem. Itaque, ipsa voluptas, a
					assumenda rem, dolorum porro accusantium, officiis veniam nostrum cum
					cumque impedit.
				</p>
				<p>
					Laborum illum ipsa voluptatibus possimus nesciunt ex consequatur rem,
					natus ad praesentium rerum libero consectetur temporibus cupiditate
					atque aspernatur, eaque provident eligendi quaerat ea soluta
					doloremque. Iure fugit, minima facere.
				</p>
			</Block>
		</Tab>
	</Tabs>
</Page>
