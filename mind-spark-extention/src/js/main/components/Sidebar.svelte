<script lang="ts">
  import { handleTabs } from "../main.svelte";


  

</script>

<nav class = "sidebar hidden" >

  <button class="sidebar-button" on:click={()=>{handleTabs("Home")}}>MindSpark</button>
  
  <div>
    <button class = "sidebar-button" on:click={()=>{handleTabs("Generative")}}>+ Add Notes</button>
    <button class = "sidebar-button" on:click={()=>{handleTabs("TTS")}}>AI Chat</button>
  </div>
  </nav>