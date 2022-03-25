<script>
  import BulletSelector from "./components/BulletSelector.svelte";
  import Goose from "./components/Goose.svelte";
  import Pirate from "./components/Pirate.svelte";
  import { state } from './store.js';

  let orientation = "bottom left"
</script>

<div class="w-screen h-screen grid">
  {#if $state == 0}
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
  {/if}
  {#if $state == 1}
  <div>
    <div class="h-full w-full grid">
      <Goose on:loose on:win/>
    </div>
  </div> 
  {/if}



</div>

<style>
  :global(body){
        background-image: url("https://cdn.pixabay.com/photo/2015/12/03/08/50/paper-1074131_1280.jpg");
    }

</style>
