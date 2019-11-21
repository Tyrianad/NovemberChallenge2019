<template>
	<div id="app" class="d-flex justify-content-center align-items-center flex-column">
		<div class="inner-container text-center">
			<h1>Christmas Countdown</h1>
			<div v-html="time"></div>
		</div>
	</div>
</template>

<script>
const christmas_date = new Date("2019-12-25");
const emojis = [
	"👶",
	"👼",
	"🎅",
	"🤶",
	"🧝‍♂️",
	"🧝‍♀️",
	"👪",
	"🦌",
	"🍪",
	"🥛",
	"🍷",
	"🍴",
	"⛪",
	"🌟",
	"❄",
	"☃",
	"⛄",
	"🔥",
	"🎄",
	"🎁",
	"🧦",
	"🔔",
	"🎶",
	"🕯",
	"🛐",
	"✝"
];

let curr_min = -1;
let curr_hour = -1;
let curr_color;
let curr_emoji;

function getFormattedFromMs(millisec) {
	if (millisec > 1000) {
		var days = Math.floor(millisec / (1000 * 60 * 60 * 24));
		var remaining_ms = millisec - days * (1000 * 60 * 60 * 24);

		var hours = Math.floor(remaining_ms / (1000 * 60 * 60));
		remaining_ms = remaining_ms - hours * (1000 * 60 * 60);

		if (hours != curr_hour) {
			curr_hour = hours;
			curr_emoji = emojis[Math.floor(Math.random() * emojis.length)];
		}

		var minutes = Math.floor(remaining_ms / (1000 * 60));
		remaining_ms = remaining_ms - minutes * (1000 * 60);

		if (minutes != curr_min) {
			curr_min = minutes;
			curr_color =
				"#" + Math.floor(Math.random() * 16777215).toString(16);
			curr_emoji = emojis[Math.floor(Math.random() * emojis.length)];
		}

		var seconds = Math.floor(remaining_ms / 1000);

		var return_str = "<h6>Time remaining until christmas:</h6>";
		return_str += "<div style='color:" + curr_color + "'>";
		return_str +=
			"<span class='round-circle border-primary'>" +
			days +
			"</span>" +
			" <strong>:</strong> ";
		return_str +=
			"<span class='round-circle border-success'>" +
			hours +
			"</span>" +
			" <strong>:</strong> ";
		return_str +=
			"<span class='round-circle border-warning'>" +
			minutes +
			"</span>" +
			" <strong>:</strong> ";
		return_str +=
			"<span class='round-circle border-info'>" +
			seconds +
			"</span><br><br>";
		return_str += "<div class='text-center'>" + curr_emoji + "</div>";
		return_str += "</div>";

		return return_str;
	} else {
		return "Oh, Ho, ho! Happy Christmas Day!";
	}
}

export default {
	name: "app",
	components: {},
	data() {
		return {
			time: getFormattedFromMs(christmas_date - new Date())
		};
	},
	created() {
		setInterval(() => {
			this.time = getFormattedFromMs(christmas_date - new Date());
		}, 1000);
	}
};
</script>

<style>
#app {
	font-family: "Mountains of Christmas", cursive;
	color: white;
	height: 100vh;
}
.inner-container {
	font-size: 18px;
	line-height: 24px;
	padding: 25px;
	border: 5px;
	border-color: #d47477 #a13134 #81272a #e7b3b4;
	border-style: solid;
	background-color: #c54245;
	border-radius: 20px;
}
.round-circle {
	display: inline-block;
	padding: 4px;
	border: 1px solid white;
	border-radius: 50%;
	width: 32px;
	height: 32px;
}
</style>