<script>
	import Bubble from './Bubble.svelte'
</script>

<div class="h-1/2 absolute bottom-0">
  <img class="h-full relative" src="images/pirate-3123711.svg" alt="Pirate"/>
  <div class="relative h-1/2 bubble">
    <Bubble
          --place-self={'start'}>
            <h2 class="relative text">How much do you dare?</h2>
    </Bubble>
  </div>
</div>

<style>
h2 {
    font-size: 2em;
    font-family: 'Shadows Into Light';
  }

  .bubble {
		border-radius: 40px;
		position: relative;
		right: -300px;
    top: -500px;
		background-size: 100%;
		}

  
  .text {
    right: -10px;
  }


</style>