<script>
	import {
		Page,
		Navbar,
		NavLeft,
		NavTitle,
		NavTitleLarge,
		NavRight,
		Link,
		Toolbar,
		Block,
		Card,
		BlockTitle,
		List,
		ListItem,
		Button,
		Searchbar,
		Tabs,
		Tab,
	} from "framework7-svelte";

	let teachers = [
		{
			id: 1,
			name: "شيخ علي العبدالكريم",
			subject: "Math",
		},
		{
			id: 2,
			name: "شيخ حسين السعيد",
			subject: "Science",
		},
		{
			id: 3,
			name: "شيخ حسن المطوع",
			subject: "English",
		},
		{
			id: 4,
			name: "شيخ أحمد المطوع",
			subject: "Arabic",
		},
		{
			id: 5,
			name: "شيخ عبدالله العبدالله",
			subject: "History",
		},
		{
			id: 6,
			name: "سيد زكريا الحاجي",
			subject: "Geography",
		},
		{
			id: 7,
			name: "سيد عبدالله الحاجي",
			subject: "Biology",
		},
		{
			id: 8,
			name: "شيخ علي الدهنين",
			subject: "Chemistry",
		},
	];

	import Form from "./form.svelte";
	let page;
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
							href="/teacher/{teacher.name}/"
							large
							outline
							style="font-size: 15px; text-align: center; color:
							black;">{teacher.name}</Button
						>
					{/each}
				</p>
			</Block>
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
