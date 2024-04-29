<script>
    import './AddNote.scss';

    const handelSubmit = () => {
        var title = document.getElementById('title').value;
        var body = document.getElementById('body').value;

        alert(`title: ${title} \n body: ${body}`)
    }
</script>

<div class="addNotes-main hidden">
    <div class="container-card">
        <div>
            <h3>Title: </h3>
            <input type="text" id="title" >
        </div>
        <div>
            <h3>Body: </h3>
            <input type="text" id="body">
        </div>

        <button type="submit" on:click={handelSubmit}>Add note</button>
    </div>
</div>