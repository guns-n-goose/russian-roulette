<script>
    import { fly } from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';
    import {kill, bullets, earnings} from '../store.js';
    
    const dispatch = createEventDispatcher();
    const looseEvent = () => { dispatch('loose') };
    const winEvent = () => { dispatch('win', { earnings }) };
    
    let b = $bullets;
    
    let goose = true;
    let roll = [];
    for (let i = 1; i <= 6; i++) {
        if (b > 0){
            roll.push(1);
            b--;
            roll = roll;
        }
        else {
            roll.push(0);
            roll = roll;
        }
    }
 
    function shoot() {
        roll = roll;
        var idx = Math.floor(Math.random() * roll.length);
        if (roll[idx] == 1) {
            kill.set(1);
            earnings.set(0);
            looseEvent();
        }
        else {
            earnings.update(n => n + 100 * 1);
        }
    }

    function endgame() {
        goose = false;
        winEvent();
    }
</script>


<div class="relative h-1/3 w-1/3 place-self-center">
    <div class="earnings absolute">
        <h2>Your earnings: {$earnings}$</h2>
    </div>
    {#if goose == true}
    <img class="h-full place-self-center" 
        in:fly="{{x: 2000, duration: 3000}}" 
        out:fly="{{x: -2000, duration: 4000}}"
        src="images/Flying_goose.svg" alt="Goose"/>
    {/if}
    {#if ! ($kill == 1) & goose == true}
    <button class="stripe" 
			on:click={shoot}>Shoot
        </button>
    <button class="end" 
        on:click={endgame}>Cash out
    </button>
    {:else if $kill == 1 & goose == true}
    <img class="absolute top-0 place-self-center" src="images/1ff5d507a5622971efd84160ae58ca85-drop-pool-blood-splatter.png" alt="blood"/>
    {/if}
</div>

<style>
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
    h2 {
    font-size: 2em;
    font-family: 'Shadows Into Light';
    }
    .earnings {
        font-size: 2.5em;
        top: -90%;
    }
</style>