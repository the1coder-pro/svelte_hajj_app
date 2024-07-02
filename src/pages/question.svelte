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
		Card,
		NavRight,
		Block,
		NavTitle,
		NavLeft,
	} from "framework7-svelte";

	import html2canvas from "html2canvas";

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

	// share the question function with web api
	function shareQuestion() {
		var onScreen = document.querySelector(".on-screen");

		html2canvas(
			onScreen,
			//  {
			// 	// onclone: function (clone) {
			// 	// 	clone.querySelector(".on-screen").style.display = "block";
			// 	// },
			// }
		).then(function (canvas) {
			// Do something with the canvas
			canvas.toBlob(async (blob) => {
				const files = [new File([blob], "image.png", { type: blob.type })];
				const shareData = {
					title: questions[0].Question,
					text: questions[0].AnswerText,
					files,
				};
				if (navigator.canShare(shareData)) {
					try {
						await navigator.share(shareData);
					} catch (err) {
						if (err.name !== "AbortError") {
							console.error(err.name, err.message);
						}
					}
				} else {
					console.warn("Sharing not supported", shareData);
				}
			});
		});
	}
</script>

<Page name="question">
	<Navbar>
		<NavLeft>
			<Button color="black" iconMaterial="share" onClick={() => shareQuestion()}
			></Button>
		</NavLeft>
		<NavTitle subtitle={mainTitle} style="font-size: 25px; padding: 20px;"
			>{subTitle}</NavTitle
		>

		<NavRight>
			<Button color="black" iconF7="arrow_right" back></Button>
		</NavRight>
	</Navbar>
	<Block class="on-screen" style="padding: 10px;">
		<h2 dir="rtl" style="text-align: center;">{questions[0].Question}</h2>
		<Card>
			<p
				dir="rtl"
				style="font-size: 20px; padding: 15px; text-justify: inter-word; text-align: justify;"
			>
				{questions[0].AnswerText}
			</p>
		</Card>
	</Block>
	<div class="off-screen" style="display: none;">
		<div
			class="image-container"
			style="  position: relative;
  display: inline-block;"
		>
			<img
				style="display: block;
  width: 100%;
  height: auto;"
				alt="background"
				src="../assets/1600w-F2CyNS5sQdM.webp"
			/>
			<div
				style="position: absolute;
  top: 20%;
  left: 50%;
  transform: translate(-50%, -50%); 
  background-color: #000000;
  color: #fff;
  padding: 10px 20px;"
				class="overlay-text"
			>
				{questions[0].Question}
			</div>
			<div
				style="position: absolute;
  top: 62%;
  left: 50%;
  transform: translate(-50%, -50%); 
  background-color: lightblue;
  color: black;
  padding: 10px 20px;"
				class="overlay-text"
			>
				{questions[0].AnswerText}
			</div>
		</div>
	</div>
</Page>
