<script>
	let chambers = [{id: "1", class: "deg-0", selected: false}, 
					{id: "2", class: "deg-60", selected: false}, 
					{id: "3", class: "deg-120", selected: false}, 
					{id: "4", class: "deg-180", selected: false}, 
					{id: "5", class: "deg-240", selected: false}, 
					{id: "6", class: "deg-300", selected: false}]
	let loaded = false;


	let selected = 0;
	

	const load = chamber => {
		chamber.selected = true;
		
	};
</script>


<div class="roll">
	{#each chambers as chamber}
			<button class="{chamber.selected ? 'loaded '+ chamber.class : 'empty ' + chamber.class}"
				on:click={() => {chamber.selected = !chamber.selected; selected = chamber.selected ? selected+1 : selected-1;}}
			></button>
	{/each}
</div>


<style>

	.roll {
		position: relative;
		top: -100px;
		right: -550px;
		background: rgb(75, 84, 87);
		border-radius: 50%;
		width: 300px;
		height: 300px;
	}

	.loaded {
	display:block;
	position:absolute;
	top:50%;
	left:51%;
	width:100px;
	height:100px;
	margin:-51px;
	background:gold;
	border-radius:51%;
	text-align:center;
	line-height:100px;
	}

	.empty {
	display:block;
	position:absolute;
	top:50%;
	left:51%;
	width:100px;
	height:100px;
	margin:-51px;
	background:rgb(158, 158, 156);
	border-radius:51%;
	text-align:center;
	line-height:100px;
	}



	.deg-0 {
	transform:translate(100px)
	}

	.deg-60 {
	transform:rotate(60deg) translate(100px) rotate(-60deg);
	}

	.deg-120 {
	transform:rotate(120deg) translate(100px) rotate(-120deg);
	}

	.deg-180 {
	transform:rotate(180deg) translate(100px) rotate(-180deg);
	}

	.deg-240 {
	transform:rotate(240deg) translate(100px) rotate(-240deg);
	}

	.deg-300 {
	transform:rotate(300deg) translate(100px) rotate(-300deg);
	}
</style>