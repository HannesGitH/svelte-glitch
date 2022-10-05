<script lang="ts">
	export let text = 'Hello world';
	export let delayMs = 0;
	// type CssAbsoluteUnit = "cm" | "mm" | "in" | "px" | "pt" | "pc";
	// type CssRelativeUnit = "em" | "ex" | "ch" | "rem" | "vw" | "vh" | "vmin" | "vmax" | "%";
	// export let height : `${number}${CssAbsoluteUnit|CssRelativeUnit}` = '96pt';
</script>

<div id="glitch-all" style="--delay: {delayMs}ms;">
	<div id="glitched1" title={text}>
		{text}
	</div>
	<div id="glitched2" title={text}>
		{text}
	</div>
	<div id="glitched3" title={text}>
		{text}
	</div>
</div>

<style lang="scss">

	#glitch-all{
		position: relative;
	}

	@mixin glitched($delayed: 0ms, $top-percent: 40%, $bottom-percent: 40%) {
		$delay: calc($delayed + var(--delay));

		// position: absolute;

		// top: -100%;
		// position: relative;
		animation: glitch 1s $delay linear infinite;

		&::before,
		&::after {
			content: attr(title);
			position: absolute;
			left: 0;
			z-index: -1;
		}

		&::before {
			// color: #ff00a2;
			$pct: $bottom-percent;
			animation: glitchTop 1s $delay linear infinite;
			clip-path: polygon(0 0, 100% 0, 100% $pct, 0 $pct);
			-webkit-clip-path: polygon(0 0, 100% 0, 100% $pct, 0 $pct);
		}

		&::after {
			// color: #00b7ff;
			$pct: calc(100% - $top-percent);
			animation: glitchBottom 1.5s $delay linear infinite;
			clip-path: polygon(0 $pct, 100% $pct, 100% 100%, 0 100%);
			-webkit-clip-path: polygon(0 $pct, 100% $pct, 100% 100%, 0 100%);
		}
	}

	#glitched1 {
		@include glitched(0ms);
		position: relative;
	}
	#glitched2 {
		@include glitched(100ms);
		top: 0%;
		position: absolute;
		color: #ff00a2;
		z-index: -1;
	}
	#glitched3 {
		@include glitched(150ms);
		position: absolute;
		top: 0%;
		color: #00d5ff;
		z-index: -2;
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
