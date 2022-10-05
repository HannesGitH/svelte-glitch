<script lang="ts">
</script>

<div id="glitched">
	<slot />
</div>

<style lang="scss">
	@import url('https://fonts.googleapis.com/css?family=Fira+Mono:400');

	#glitched {
		font-size: 96px;
		font-family: 'Fira Mono', monospace;
		letter-spacing: -7px;
		animation: glitch 1s linear infinite;

		& :before,
		& :after {
			content: attr(title);
			position: absolute;
			left: 0;
		}

		& :before {
			animation: glitchTop 1s linear infinite;
			clip-path: polygon(0 0, 100% 0, 100% 33%, 0 33%);
			-webkit-clip-path: polygon(0 0, 100% 0, 100% 33%, 0 33%);
		}

		& :after {
			animation: glitchBottom 1.5s linear infinite;
			clip-path: polygon(0 67%, 100% 67%, 100% 100%, 0 100%);
			-webkit-clip-path: polygon(0 67%, 100% 67%, 100% 100%, 0 100%);
		}
	}

	@keyframes glitch {
		2%,
		64% {
			transform: translate(2px, 0) skew(0deg);
		}
		4%,
		60% {
			transform: translate(-2px, 0) skew(0deg);
		}
		62% {
			transform: translate(0, 0) skew(5deg);
		}
	}

	@keyframes glitchTop {
		2%,
		64% {
			transform: translate(2px, -2px);
		}
		4%,
		60% {
			transform: translate(-2px, 2px);
		}
		62% {
			transform: translate(13px, -1px) skew(-13deg);
		}
	}

	@keyframes glitchBottom {
		2%,
		64% {
			transform: translate(-2px, 0);
		}
		4%,
		60% {
			transform: translate(-2px, 0);
		}
		62% {
			transform: translate(-22px, 5px) skew(21deg);
		}
	}
</style>
