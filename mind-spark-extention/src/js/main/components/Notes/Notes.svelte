<script>
  import { handleTabs, setMyNoteBody, setMyNoteTitle } from '../../main.svelte';


  import './Notes.scss';
    var notes;
    notes = [
        {id: 0, title: "note title1", body: "note body1"},
        {id: 1, title: "note title2", body: "note body2"},
        {id: 2, title: "note title3", body: "note body3"},
        {id: 3, title: "note title4", body: "note body4"},
        {id: 4, title: "note title4", body: "note body4"},
        {id: 5, title: "note title4", body: "note body4"},
        ]
        

</script>

<div class="notes-main hidden">
    {#if !notes}
    <p>You don't have any notes yet. Why don't you create one?</p>
    {/if}
    
    <div class="notes-container">
        
        {#each notes as note}
        <div class="notes-row">
            <button class="note-card" on:click={()=>{setMyNoteTitle(note.title); setMyNoteBody(note.body); handleTabs('EditNote', note)}}>
                <h2>{note.title}</h2>
                <p>{note.body}</p>
            </button>
        </div>
        {/each}
    </div>
</div>

