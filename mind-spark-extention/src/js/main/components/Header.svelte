<script lang="ts">

    import { handleTabs } from "../main.svelte";


</script>

<header class="app-header">
  <div>
    <img src="/assets/logo.png" alt="MindSpark logo" width={100} height={100}/>
    <h1>MindSpark</h1>
  </div>
  <h3>An inteligent note-taking app ai integration</h3>
  <button on:click={()=>{handleTabs("Notes")}}>
    Open
  </button>
</header>