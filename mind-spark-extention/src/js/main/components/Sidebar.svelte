<script lang="ts">
  import { handleTabs } from "../main.svelte";


  

</script>

<nav class = "sidebar hidden" >

  <button class="sidebar-button" on:click={()=>{handleTabs("Notes")}}>MindSpark</button>
  
  <div>
    <button class = "sidebar-button" on:click={()=>{handleTabs("AddNote")}}>+ Add Notes</button>
    <button class = "sidebar-button" on:click={()=>{handleTabs("Chat")}}>AI Chat</button>
  </div>
  </nav>