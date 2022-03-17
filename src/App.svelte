<script>
  import { fade } from "svelte/transition";
  import Pirate from "components/Pirate.svelte"

  let name = "World";
  let orientation = "bottom left"
</script>

<main class="w-full h-full" transition:fade>
  <Pirate></Pirate>

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
