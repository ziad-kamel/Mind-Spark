<script>
  import { token, userId } from '../../main.svelte';
  import './Chat.scss';
    var userPrompt = ''
    var responses = ''

    const handelSubmit = async () => {
        responses = ''
        var prompt = document.getElementById('prompt').value;
        userPrompt = prompt
        
        var myHeaders = new Headers();
        myHeaders.append("Authorization", `Bearer ${token}`);
        myHeaders.append("userId", `${userId}`);

        const botResponse = await fetch(`http://localhost:3000/api/chat`,{
            method:"POST",
            headers: myHeaders,
            body: JSON.stringify({messages: [{content: userPrompt, role: "assistant"}]})
        }).then((res)=>{return res.text()}).catch((error)=>{alert(error.message)})
        responses = botResponse
    }


</script>

<div class="chat-main hidden">
    <div class="chat-container">
        <div class="chat-body">
            <div class="message-row">
                <p class="message"> {userPrompt}</p>
            </div>
            <div class="response-row">
                <p class="response"> {responses}</p>
            </div>
        </div>

        <div class="chat-controls">
            <button>bin</button>
            <input type="text" id="prompt" placeholder="Say something...">
            <button type="submit" on:click={handelSubmit}>Send</button>
        </div>
    </div>
</div>