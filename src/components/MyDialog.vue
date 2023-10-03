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
				<ShareNetwork
					style=" background-color: dodgerblue; color: darkblue; z-index: 91"
					network="twitter"
					url="https://built.africa"
					title="Say hi to Vite! A brand new, extremely fast development setup for Vue."
					description="This week, I’d like to introduce you to 'Vite', which means 'Fast'. It’s a brand new development setup created by Evan You."
					quote="The hot reload is so fast it\'s near instant. - Evan You"
					hashtags="vuejs,vite"
				>
					Share on Facebook
				</ShareNetwork>
			</div>
			<div v-else>
				<h1>Sorry 😬. Better luck next time. </h1>
			</div>
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
	z-index: 90;
	min-height: 100vh;
	background-color: rgba(0, 0, 0, 0.5);
	display: flex;
	align-items: center;
	justify-content: center;
}

div {
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