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
		Card,
		CardContent,
		CardHeader,
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

	import { onMount } from "svelte";

	let popupOpened = false;

	// get questions from data.json
	let questions = [];
	import data from "./data.json";
	data.forEach((question) => {
		questions.push(question);
	});

	// load ads from the url https://opensheet.elk.sh/1IR-c-DM1_G0Qr6sr-iy7gZKwWN5zuQfo_Vr8Ky29BgE/1
	let ads = [];
	const url =
		"https://opensheet.elk.sh/1IR-c-DM1_G0Qr6sr-iy7gZKwWN5zuQfo_Vr8Ky29BgE/1";

	onMount(async () => {
		const response = await fetch(url);
		ads = await response.json();
	});

	function getImageLink(ad) {
		// if the link is from google drive, get the image id and return the link

		if (ad.Image.toString().includes("drive.google.com")) {
			var id = ad.Image.toString().split("id=")[1];
			return `https://lh3.googleusercontent.com/d/${id}=s1000?authuser=0`;
		} else {
			return ad.Image;
		}
	}

	import { register } from "swiper/element/bundle";

	register();
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
							black;"
							><h3>
								{teacher}
							</h3>
						</Button>
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
						<Searchbar
							placeholder="البحث"
							searchContainer=".search-list"
							searchIn=".item-title"
						/>
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
			<swiper-container
				pagination={true}
				class="demo-swiper-multiple"
				loop={true}
				autoplay={true}
				space-between={50}
			>
				{#each ads as ad}
					<swiper-slide>
						<img
							src={getImageLink(ad)}
							alt={ad.Title}
							style="width: 100%; height: 200px;"
						/>
					</swiper-slide>
				{/each}
			</swiper-container>
			<div class="demo-expandable-cards">
				{#each ads as ad}
					<Card expandable>
						<CardContent padding={false}>
							<div
								style="background: url({getImageLink(
									ad,
								)}) no-repeat center bottom; background-size: cover; height: 240px"
							/>
							<Link
								cardClose
								color="white"
								class="card-opened-fade-in"
								style="position: absolute; right: 15px; top: 15px"
								iconF7="xmark_circle_fill"
							/>
							<CardHeader dir="rtl" style="height: 60px; padding-right: 40px;"
								>{ad.Title}</CardHeader
							>
							<div class="card-content-padding" dir="rtl">
								<p>
									{ad.Description}
								</p>

								<Link iconMaterial="launch" href={ad.Link} external></Link>

								<p>
									<Button fill round large cardClose>إغلاق الإعلان</Button>
								</p>
							</div>
						</CardContent>
					</Card>
				{/each}
			</div>
		</Tab>
	</Tabs>
</Page>
