<svelte:head>
    <title>Russian Roulette</title>
</svelte:head>

<script>
  import { fly } from 'svelte/transition';
  import { createEventDispatcher } from 'svelte';
  import {state, bullets, kill, earnings} from './store.js';

	let chambers = [{id: "1", class: "deg-0", selected: true}, 
					{id: "2", class: "deg-60", selected: false}, 
					{id: "3", class: "deg-120", selected: false}, 
					{id: "4", class: "deg-180", selected: false}, 
					{id: "5", class: "deg-240", selected: false}, 
					{id: "6", class: "deg-300", selected: false}]

	bullets.set(1);

  export let tickSize = 24
	
	let Width = 300
  let Height = 100
  
  const dispatch = createEventDispatcher();
  const loseEvent = () => { dispatch('lose', { amount: 'all' }) };
  const winEvent = () => { dispatch('win', { amount: $earnings }) };
  
  let b = $bullets;
  
  let goose = true;
  let roll = [];

  for (let i = 1; i <= 6; i++) {
    if (b > 0){
        roll.push(1);
        b--;
    }
    else {
        roll.push(0);
    }
}
  
  function shoot() {
      roll = roll;
      var idx = Math.floor(Math.random() * roll.length);
      if (roll[idx] == 1) {
          kill.set(1);
          earnings.set(0);
          loseEvent();
      }
      else {
          earnings.update(n => n + 100 * 1);
      }
  }

  function update_roll(chamber_is_selected) {

    if (chamber_is_selected) {
      let idx = roll.indexOf(0);
      roll[idx] = 1;

      bullets.update(n => n + 1)
    }
    else {
      let idx = roll.indexOf(1);
      roll[idx] = 0;

      bullets.update(n => n - 1)
    }
  }

  function endgame() {
      goose = false;
      winEvent();
      
  }
</script>

<div class="w-full h-full grid">
  {#if $state == 0}
    <div class="w-1/2 h-full place-self-center">
      <div class="w-full h-1/2 grid">
        <div class="place-self-center">
          <div class="roll">
            {#each chambers as chamber}
                <button class="{chamber.selected ? 'loaded '+ chamber.class : 'empty ' + chamber.class}"
                  on:click={() => {chamber.selected = !chamber.selected; 
                           update_roll(chamber.selected)}}
                ></button>
            {/each}
            {#if $bullets == 6}
            <div class="death">
              <img src="https://raw.githubusercontent.com/guns-n-goose/russian-roulette-game/v.0.2/public/images/sugar-skull-1782019.svg" alt="Instant death">
              <h2 style="position:relative; right:-300px; top:-150px;">Are you suicidal, mate?</h2>
            </div>
            {:else if $bullets == 0}
            <div class="death">
              <h2 style="position:relative; right:300px; top:-150px;">Scared, are we?</h2>
            </div>
            {:else}
            <button class="stripe" 
                on:click={() => state.set(1)}>Ready</button>
            {/if}	
          </div>
        </div>
      </div>
      <div class="w-full h-1/2 grid">
        <div class="h-1/2 place-self-center">
          <div class="h-1/2 absolute bottom-0 right-60">
            <img class="h-full relative" src="https://raw.githubusercontent.com/guns-n-goose/russian-roulette-game/v.0.2/public/images/pirate-3123711.svg" alt="Pirate"/>
            <div class="relative h-1/2 bubble">
              <div class="bubble2" >
                <svg width={Width} height={Height} viewBox="0 0 {Width} {Height}">
                  <rect x=0 y=0 width={Width} height={Height} rx=5/>
                  
                      <path d="M{tickSize*2},{Height} h-{tickSize} v{tickSize} Z"/>
                </svg>
                <h2 class="relative text">How much do you dare?</h2>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  {/if}
  {#if $state == 1}
  <div>
    <div class="h-full w-full grid">
      <div class="relative h-1/3 w-1/3 place-self-center">
        <div class="earnings absolute">
            <h2>Your earnings: {$earnings}$</h2>
        </div>
        {#if goose == true}
        <img class="h-full place-self-center" 
            in:fly="{{x: 2000, duration: 3000}}" 
            out:fly="{{x: -2000, duration: 4000}}"
            src="https://raw.githubusercontent.com/guns-n-goose/russian-roulette-game/v.0.2/public/images/Flying_goose.svg" alt="Goose"/>
        {/if}
        {#if ! ($kill == 1) & goose == true}
        <button class="stripe" 
          on:click={shoot}>Shoot
            </button>
        <button class="end" 
            on:click={endgame}>Cash out
        </button>
        {:else if $kill == 1 & goose == true}
        <img class="absolute top-0 place-self-center" src="https://raw.githubusercontent.com/guns-n-goose/russian-roulette-game/v.0.2/public/images/1ff5d507a5622971efd84160ae58ca85-drop-pool-blood-splatter.png" alt="blood"/>
        {/if}
    </div>
    
    </div>
  </div> 
  {/if}



</div>

<style>
  :global(body){
        background-image: url("https://cdn.pixabay.com/photo/2015/12/03/08/50/paper-1074131_1280.jpg");
    }
  
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

    .bubble {
    border-radius: 40px;
    position: relative;
    right: -500px;
    top: -700px;
    background-size: 100%;
    }

    .bubble2 {
		place-self: start;
	}

  .text {
    right: -10px;
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
    
    .end {
		border-radius: 40px;
		position: relative;
		font-size: 3em;
    	font-family: 'Shadows Into Light';
		right: -200px;
		height: 100px;
		width: 200px;
		border: 2px solid #000000;
		color: #000000;
		background-image: repeating-linear-gradient(90deg, 
			rgba(20, 25, 25, 0.6),
			rgba(128, 182, 59, 0.6) 10%, 
			#a9f38b 10%, #008a0b 20%);
		background-size: 100%;
		transition: background 0.3s ease-in-out;
		}
	.end:hover {
		background-position: 150px;
		}
   
    .earnings {
        font-size: 2.5em;
        top: -90%;
    }

</style>
