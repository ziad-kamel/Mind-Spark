<script>
  import { handleTabs, setMyNote, setMyNoteContent, setMyNoteTitle, token, userId } from '../../main.svelte';


  import './Notes.scss';
    var allNotes = false;
    var message = "You don't have any notes yet. Why don't you create one?"
        const handleRefresh = async () => {
            message = "loading..."
            var myHeaders = new Headers();
            myHeaders.append("Authorization", `Bearer ${token}`);
            myHeaders.append("userId", `${userId}`);
            var res = await fetch(`http://localhost:3000/api/notes`, {
                method: "GET",
                headers: myHeaders
            }).then((response)=> {return response.json()}).catch((err)=>{alert(err.message)})
            allNotes = res.notes
            allNotes.reverse();
        }
</script>

<div class="notes-main hidden">
    <button id="refresh" on:click={handleRefresh}></button>
    {#if !allNotes}
    <p>{message}</p>
    {/if}
    
    <div class="notes-container">
        {#each allNotes as note}
        <div class="notes-row">
            <button class="note-card" on:click={()=>{setMyNote(note) ;setMyNoteTitle(note.title); setMyNoteContent(note.content); handleTabs('EditNote', note)}}>
                <h2>{note.title}</h2>
            </button>
        </div>
        {/each}
    </div>
</div>

