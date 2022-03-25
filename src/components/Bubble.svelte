<script>
	import { scale } from 'svelte/transition'
	import { elasticInOut } from 'svelte/easing'
	export let tickSize = 24
	
	let Width = 300
    let Height = 100
</script>

<div class="bubble" >
	<svg width={Width} height={Height} viewBox="0 0 {Width} {Height}">
		<rect x=0 y=0 width={Width} height={Height} rx=5/>
		
        <path d="M{tickSize*2},{Height} h-{tickSize} v{tickSize} Z"/>
	</svg>
	<slot/>
</div>

<style>
	.bubble {
		place-self: var(--place-self)
	}
	
	.bubble svg {
		overflow: visible;
		position: var(--position, absolute);
		left: var(--left, 0);
		z-index: -1;
	}
	
	rect, path {
		fill: var(--fill-color, rgba(255, 255, 255, 0));
        stroke: #000000;
        stroke-width: 3px;
        stroke-linejoin: round;
	}
</style>