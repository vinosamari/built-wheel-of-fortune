<script>
import Confetti from "@/components/Confetti.vue";

export default {
	name: "MyDialog",
	components: {Confetti},
	props: ['prize']
}
</script>

<template>
	<main>
		<confetti :value="prize.value"/>
		<section>
			<div v-if="prize.id !== 6">
				<h1>Congratulations!🎉🎉</h1>
				<h2>You've won {{ prize.value }}!</h2>
			</div>
			<div v-else>
				<h1>Sorry 😬. Better luck next time. </h1>
			</div>
<!--			<ShareNetwork-->
<!--				style=" background-color: royalblue; color: whitesmoke; z-index: 998; text-decoration: none; padding: 10px 20px; font-weight: bold; margin: 0 10px; border-radius: 10px"-->
<!--				network="facebook"-->
<!--				url="https://built.africa"-->
<!--				:title="`Look! I just won ${prize.value} from Built!`"-->
<!--				description="All i had to do was spin the wheel of fortune!"-->
<!--				quote="I'm so excited!"-->
<!--				hashtags="built, builtforyou, builttowin"-->
<!--			>-->
<!--				Share on Facebook-->
<!--			</ShareNetwork>-->
<!--			<ShareNetwork-->
<!--				style=" background-color: black; color: whitesmoke; z-index: 998; text-decoration: none; padding: 10px 20px; font-weight: bold; border-radius: 10px;  margin: 0 10px;"-->
<!--				network="twitter"-->
<!--				url="https://built.africa"-->
<!--				:title="`Look! I just won ${prize.value} from Built!`"-->
<!--				description="All i had to do was spin the wheel of fortune!"-->
<!--				quote="I'm so excited!"-->
<!--				hashtags="built, builtforyou, builttowin"-->
<!--			>-->
<!--				Share on X-->
<!--			</ShareNetwork>-->
<!--			<ShareNetwork-->
<!--				style=" background-color: seagreen; color: whitesmoke; z-index: 998; text-decoration: none; padding: 10px 20px; font-weight: bold; border-radius: 10px;  margin: 0 10px;"-->
<!--				network="whatsapp"-->
<!--				url="https://built.africa"-->
<!--				:title="`Look! I just won ${prize.value} from Built!`"-->
<!--				description="All i had to do was spin the wheel of fortune!"-->
<!--				quote="I'm so excited!"-->
<!--				hashtags="built, builtforyou, builttowin"-->
<!--			>-->
<!--				Share on Whatsapp-->
<!--			</ShareNetwork>-->
		</section>
	</main>
</template>

<style scoped>
section {
	position: absolute;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	z-index: 98;
	min-height: 100vh;
	background-color: rgba(0, 0, 0, 0.5);
	display: flex;
	align-items: center;
	justify-content: center;
}

div {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	background-color: white;
	padding: 50px;
	width: 100vw;
	height: 100vh;
	border-radius: 20px;
}

h1 {
	font-weight: bolder;
	font-size: 2rem;
}
</style>