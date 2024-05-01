<script >
  import { myNote, token, userId } from '../../main.svelte';
  import './EditNote.scss';
  var title;
  var content;
  var noteId;
    const handleRefresh = () => {
        title = myNote.title
        content = myNote.content
        noteId = myNote.id
    }

    const handleSubmit = async () => {
            var myHeaders = new Headers();
            myHeaders.append("Authorization", `Bearer ${token}`);
            myHeaders.append("userId", `${userId}`);
            const response = await fetch(`http://localhost:3000/api/notes`,{
                method:"PUT",
                headers: myHeaders,
                body: JSON.stringify({id: noteId, title: title, content: content})
            }).then((res)=>{return res.json()}).catch((error)=>{alert(error.message)})

            if(response.updatedNote){
                alert('note updated successfully \n refresh all notes and see the updated note')
            } else {
                alert('something went wrong while updating')
            }
        }
    const handelDelete = async () => {
            var myHeaders = new Headers();
            myHeaders.append("Authorization", `Bearer ${token}`);
            myHeaders.append("userId", `${userId}`);
            const response = await fetch(`http://localhost:3000/api/notes`,{
                method:"DELETE",
                headers: myHeaders,
                body: JSON.stringify({id: noteId})
            }).then((res)=>{return res.json()}).catch((error)=>{alert(error.message)})

            if(response.message){
                alert('note deleted successfully \n refresh the all notes and it will be gone')
            } else {
                alert('something went wrong while deleting')
            }
    }
</script>
<div class="edit-main hidden">
    <p>note: if the values not showing try  <button on:click={handleRefresh}>refresh</button></p>
    <div class="note">
        <div class="title">
            <h3>Title: </h3>
            <input type="text" bind:value={title}>
        </div>
        <div class="content">
            <h3>content: </h3>
            <input type="text" bind:value={content}>
        </div>
        <div class="action-buttons">
            <button on:click={handelDelete} class="delete-btn">delete</button>
            <button on:click={handleSubmit}>submit</button>
        </div>
    </div>
</div>