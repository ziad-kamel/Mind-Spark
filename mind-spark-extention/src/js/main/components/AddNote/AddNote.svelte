<script>
  import { token, userId } from '../../main.svelte';
  import './AddNote.scss';

  var buttonState = "Add note"
    const handelSubmit = async () => {
        buttonState = 'adding...'
        var title = document.getElementById('title').value;
        var content = document.getElementById('content').value;

        alert(`title: ${title} \n content: ${content}`)

        var myHeaders = new Headers();
        myHeaders.append("Authorization", `Bearer ${token}`);
        myHeaders.append("userId", `${userId}`);
        const response = await fetch(`https://mind-spark-v1qx.vercel.app/api/notes`,{
            method:"POST",
            headers: myHeaders,
            body: JSON.stringify({title: title,content: content})
        }).then((res)=>{return res.json()}).catch((error)=>{alert(error.message); buttonState = 'Add Note'})
        alert(JSON.stringify(response.note))
        if(response.note){
            alert('note added successfully')
        } else {
            alert('something wrong happened')
        }
        buttonState = 'Add note'
        handleTabs("Notes")
    }
</script>

<div class="addNotes-main hidden">
    <div class="container-card">
        <div>
            <h3>Title: </h3>
            <input type="text" id="title" >
        </div>
        <div>
            <h3>Content: </h3>
            <input type="text" id="content">
        </div>

        <button type="submit" on:click={handelSubmit}>{buttonState}</button>
    </div>
</div>