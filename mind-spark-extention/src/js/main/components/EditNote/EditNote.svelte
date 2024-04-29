<script >
  import { myNoteBody, myNoteTitle } from '../../main.svelte';
  import './EditNote.scss';
  var title;
  var body;
    const handleRefresh = () => {
        title = myNoteTitle
        body = myNoteBody
    }

    const handleSubmit = () => {
        alert(title)
        alert(body)
    }
</script>
<div class="edit-main hidden">
    <p>note: if the values not showing try  <button on:click={handleRefresh}>refresh</button></p>
    <div class="note">
        <div class="title">
            <h3>Title: </h3>
            <input type="text" bind:value={title}>
        </div>
        <div class="body">
            <h3>Body: </h3>
            <input type="text" bind:value={body}>
        </div>
        <button on:click={handleSubmit}>submit</button>
    </div>
</div>