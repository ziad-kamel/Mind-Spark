<script>
  import "./AudioCleanup.scss";

  var file;
  var audioUrl;
  var denoisedAudio;
  var enhancedAudio;

  const setFile = async (inputFile) => {
    file = inputFile;
  };

</script>

<div class="cleanup-main hidden">
  <h1>Audio Cleanup</h1>
  <input
    type="file"
    on:change={(e) => {
      setFile(e.target.files?.[0]);
    }}
  />
  <button class="sidebar-button" >Generate</button>

  <div>
    {#if denoisedAudio && enhancedAudio}
      <audio controls>
        <source src={denoisedAudio} type="audio/mpeg" />
      </audio>

      <audio controls>
        <source src={enhancedAudio} type="audio/mpeg" />
      </audio>
    {/if}
  </div>
</div>
