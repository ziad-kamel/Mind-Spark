<script context="module">
  import {
    Audio_Generation_Version,
    Normalization_Strategy,
  } from "../../../lib/utils/types";
  import './GenerativeAudio.scss';


  

  let prompt;
  let version;
  let strategy;
  let duration =1;
  let output = "";


</script>



<div class="generative-content">
    <div >
      <textarea bind:value={prompt} placeholder="Enter the prompt"></textarea>
    </div>

    <div class="audio-gen-options">
      <div>
        <p style = "display: inline">Version: </p>
          <select bind:value={version}> 
              <option value="" disabled selected hidden>select a version</option>
              {#each Audio_Generation_Version as modelName}
                <option>{modelName.model_version}</option>
              {/each}
          </select>
      </div>

      <div>
        <p style = "display: inline"> Strategy: </p>
          <select bind:value={strategy}> 
            <option value="" disabled selected hidden>select a strategy</option>
            {#each Normalization_Strategy as strategy}
              <option>{strategy.strategy}</option>
            {/each}
          </select>
      </div>
      <div>
        <p style="display: inline">Duration: </p><input bind:value={duration} type="number" min=3 max=20 />
      </div>
    </div>
    <div class="generate-btn">
      <button class= "sidebar-button" type="submit" on:click={() =>{}} >Generate</button>
    </div>
    <div class="audio-output">
    </div>  
  </div>