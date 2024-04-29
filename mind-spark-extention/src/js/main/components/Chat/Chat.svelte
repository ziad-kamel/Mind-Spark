<script>
  import './Chat.scss';
    // var messages = ["tell me a joke!", "tell me a new joke!", "tell me another joke!"]
    // var responses = ["xavi hernandes", "pep goudriola", "diago semioni"]
    var messages = ''
    var responses = ''


    var c = 1;
    const handelSubmit = async () => {
        responses = ''
        var prompt = document.getElementById('prompt').value;
        messages = prompt
        responses = 'ayy yo brooo' + c++
        // messages.push(prompt)
    }


</script>

<div class="chat-main hidden">
    <div class="chat-container">
        <div class="chat-body">
            <div class="message-row">
                <p class="message"> {messages}</p>
            </div>
            <div class="response-row">
                <p class="response"> {responses}</p>
            </div>

            <!-- <div class="message-col">
                {#each responses as response}
                <p class="response">{response}</p>
                {/each}
            </div>
            <div class="response-col">
                {#each messages as message}
                <p class="message">{message}</p>
                {/each}
            </div> -->
        </div>

        <div class="chat-controls">
            <button>bin</button>
            <input type="text" id="prompt" placeholder="Say something...">
            <button type="submit" on:click={handelSubmit}>Send</button>
        </div>
    </div>
</div>