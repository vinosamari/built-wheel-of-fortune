<script>
export default {
	name: "Confetti",
	props: ['value'],
	mounted() {
		// Create a new audio object
		let happyAudio = new Audio(require('../assets/crowd.mp3'));
		let sadAudio = new Audio(require('../assets/sad-crowd.mp3'));
		let pop = new Audio(require("../assets/pop.mp3"));
		pop.volume = 0.2;

		// Set the volume
		happyAudio.volume = 0.6;
		sadAudio.volume = 0.6;
		console.log(this.value)
		// Play the audio
		this.value !== 'Nothing' ? happyAudio.play() && pop.play() : sadAudio.play()
		if(this.value === 'Nothing') return

		const canvas = document.getElementById("canvas");
		const ctx = canvas.getContext("2d");

		canvas.width = window.innerWidth;
		canvas.height = window.innerHeight;

		const confettiColors = [
			"#f44336",
			"#e91e63",
			"#9c27b0",
			"#673ab7",
			"#3f51b5",
			"#2196f3",
			"#03a9f4",
			"#00bcd4",
			"#009688",
			"#4caf50",
			"#8bc34a",
			"#cddc39",
			"#ffeb3b",
			"#ffc107",
			"#ff9800",
			"#ff5722",
			"#795548"
		];

		const confettiShapes = ["circle", "square", "triangle", "heart"];

		class Confetti {
			constructor() {
				this.color =
					confettiColors[Math.floor(Math.random() * confettiColors.length)];
				this.shape =
					confettiShapes[Math.floor(Math.random() * confettiShapes.length)];
				this.size = Math.random() * 20 + 10;
				this.x = Math.random() * canvas.width;
				this.y = -this.size;
				this.velocityX = Math.random() * 4 - 2;
				this.velocityY = Math.random() * 4 + 6;
				this.rotation = Math.random() * 360;
				this.rotationSpeed = Math.random() * 4 - 2;
			}

			update() {
				this.x += this.velocityX;
				this.y += this.velocityY;
				this.rotation += this.rotationSpeed;

				if (this.x > canvas.width + this.size) {
					this.x = -this.size;
				} else if (this.x < -this.size) {
					this.x = canvas.width + this.size;
				}

				if (this.y > canvas.height + this.size) {
					this.y = -this.size;
				}
			}

			draw() {
				ctx.save();
				ctx.fillStyle = this.color;
				ctx.translate(this.x + this.size / 2, this.y + this.size / 2);
				ctx.rotate((this.rotation * Math.PI) / 180);
				switch (this.shape) {
					case "circle":
						ctx.beginPath();
						ctx.arc(0, 0, this.size / 2, 0, 2 * Math.PI);
						ctx.fill();
						break;
					case "square":
						ctx.fillRect(-this.size / 2, -this.size / 2, this.size, this.size);
						break;
					case "triangle":
						ctx.beginPath();
						ctx.moveTo(0, -this.size / 2);
						ctx.lineTo(this.size / 2, this.size / 2);
						ctx.lineTo(-this.size / 2, this.size / 2);
						ctx.fill();
						break;
					case "heart":
						ctx.beginPath();
						ctx.moveTo(0, -this.size / 4);
						ctx.quadraticCurveTo(this.size / 2, -this.size / 2, 0, this.size / 2);
						ctx.quadraticCurveTo(-this.size / 2, -this.size / 2, 0, -this.size / 4);
						ctx.fill();
						break;
				}
				ctx.restore();
			}
		}

		const confettis = [];
		const maxConfettis = 500;

		function createConfetti(amount) {
			for (let i = 0; i < amount; i++) {
				const confetti = new Confetti();
				confettis.push(confetti);
			}
		}

		createConfetti(50);

		function animateConfetti() {
			ctx.clearRect(0, 0, canvas.width, canvas.height);

			for (let i = 0; i < confettis.length; i++) {
				const confetti = confettis[i];
				confetti.update();
				// remove older confetti if the number of confettis is greater than maxConfettis
				while (confettis.length > maxConfettis) confettis.shift();
				// remove confetti that has gone off screen
				if (confetti.y > canvas.height + confetti.size) {
					confettis.splice(i, 1);
					i--;
					continue;
				}

				confetti.draw(ctx);
			}

			requestAnimationFrame(animateConfetti);
		}

		animateConfetti();

		const addConfetti = () => {
			setTimeout(() => {
				ctx.clearRect(0, 0, canvas.width, canvas.height);
				createConfetti(Math.floor(Math.random() * 50) + 50);
			}, 500);
		};

		const clearConfetti = () => {
			confettis.splice(0, confettis.length);
			animateConfetti();
		};


// Create a function to handle key presses
		function handleKeyPress(event) {
			// Check if the pressed key is "F"
			if (event.key === "f" || event.key === "F") {
				// Perform an action when the "F" key is pressed
				if (document.fullscreenElement) document.exitFullscreen();
				else document.documentElement.requestFullscreen();
			}
			if (event.key === "a" || event.key === "A") addConfetti();
			if (event.key === "c" || event.key === "C") clearConfetti();
		}
// Add an event listener to trigger the function when a key is pressed
		document.addEventListener("keydown", handleKeyPress);

		window.addEventListener(
			"resize",
			() => {
				canvas.width = window.innerWidth;
				canvas.height = window.innerHeight;
			},
			false
		);

	}
}
</script>

<template>
	<div>
		<canvas id="canvas"></canvas>
	</div>
</template>

<style scoped>
canvas {
	background-color: transparent;
	position: absolute;
	top: 0;
	left: 0;
	z-index: 999;
}

.confetti {
	position: absolute;
	width: 10px;
	height: 10px;
	border-radius: 50%;
	opacity: 0.7;
}

button {
	background-color: #4caf50; /* Green */
	border: none;
	color: white;
	text-align: center;
	text-decoration: none;
	display: inline-block;
	font-size: 16px;
	margin: 4px 2px;
	cursor: pointer;
}

button:hover {
	background-color: #3e8e41;
}

.visibility {
	opacity: 0;
	transition-delay: 3s;
}

.visibility:hover {
	transition-delay: 0s;
	opacity: 1;
}

</style>