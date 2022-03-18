<script>
  import { fade } from "svelte/transition";
  import Bubble from "components/Bubble.svelte"
  import BulletSelector from "./components/BulletSelector.svelte";
  import Pirate from "./components/Pirate.svelte";

  let name = "World";
  let orientation = "bottom left"
</script>

<!--
<main class="w-full h-full" transition:fade>
  <div class="pirate flex flex-col">
    <div>
      <img src="images/pirate-3123711.svg" alt="Pirate" style="width:300px;"/>
    </div>
    <div class="w-full h-full" style="width:300px; height:100px;">
      <Bubble
        --place-self={'start'}>
          <h2>How much do you dare?</h2>
      </Bubble>
    </div>
    <div><BulletSelector/></div>
  </div>
</main>
-->

<div class="w-screen h-screen grid">
  <div class="w-1/2 h-full place-self-center">
    <div class="w-full h-1/2 grid">
      <div class="place-self-center">
        <BulletSelector/>
      </div>
    </div>
    <div class="w-full h-1/2 grid">
      <div class="h-1/2 place-self-center">
        <Pirate/>
      </div>
    </div>
  </div>
</div>

<style>
  :global(body){
        background-image: url("https://cdn.pixabay.com/photo/2015/12/03/08/50/paper-1074131_1280.jpg");
    }

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
