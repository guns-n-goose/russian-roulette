<script>
  import { fade } from "svelte/transition";
  import Bubble from "components/Bubble.svelte"
  import BulletSelector from "./components/BulletSelector.svelte";

  let name = "World";
  let orientation = "bottom left"
</script>

<main class="w-full h-full" transition:fade>
  <div class="Pirate">
    <img src="images/pirate-3123711.svg" alt="Pirate" style="display:block; width:300px; margin-left:auto; margin-right:auto; margin-top:80px;"/>
      <div class="w-full h-full" style="position:relative; top:-425px; right:-780px; width:300px; height:100px;">
        <Bubble
          --place-self={'start'}>
            <h2>How much do you dare?</h2>
        </Bubble>
      </div>
  </div>
  <BulletSelector/>


</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  h2 {
    font-size: 2em;
    font-family: 'Shadows Into Light';
  }
</style>
