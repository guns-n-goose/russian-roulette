<script>
	let chambers = [{id: "1", class: "deg-0", selected: true}, 
					{id: "2", class: "deg-60", selected: false}, 
					{id: "3", class: "deg-120", selected: false}, 
					{id: "4", class: "deg-180", selected: false}, 
					{id: "5", class: "deg-240", selected: false}, 
					{id: "6", class: "deg-300", selected: false}]
	let loaded = false;


	let selected = 1;
	

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
	{#if selected == 6}
	<div class="death">
		<img src="images/sugar-skull-1782019.svg" alt="Instant death">
		<h2 style="position:relative; right:-300px; top:-150px;">Are you suicidal, mate?</h2>
	</div>
	{:else if selected == 0}
	<div class="death">
		<h2 style="position:relative; right:300px; top:-150px;">Scared, are we?</h2>
	</div>
	{:else}
	<button class="stripe">Ready</button>
	{/if}	
</div>



<style>
	
	h2 {
    font-size: 2em;
    font-family: 'Shadows Into Light';
  }
	.roll {
		position: relative;
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

	.death {
		position:relative; 
		top:100px; 
		right:-120px; 
		width:70px; 
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

	.stripe {
		border-radius: 40px;
		position: relative;
		font-size: 3em;
    	font-family: 'Shadows Into Light';
		right: 200px;
		height: 100px;
		width: 200px;
		border: 2px solid #000000;
		color: #000000;
		background-image: repeating-linear-gradient(90deg, 
			rgba(20, 25, 25, 0.6),
			rgba(25, 25, 25, 0.6) 10%, 
			#4c4c4c 10%, #4c4c4c 20%);
		background-size: 100%;
		transition: background 0.3s ease-in-out;
		}

	.stripe:hover {
		background-position: 150px;
		}
</style>