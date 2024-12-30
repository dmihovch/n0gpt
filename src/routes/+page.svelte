<script>
    let msgResp = $state("nothing");
    let loading = $state(false);
    let prompt = $state("");
    
    async function promptGemini(){
        loading = true;
        const promptStr = prompt;
        const response = await fetch(`/api/gemini?query=${encodeURIComponent(promptStr)}`);
        const result = await response.text();
        loading = false;
        msgResp = result;
        prompt = "";
    }
</script>

<div>
    <form onsubmit={promptGemini}>
        <label for="input">Ask me anything!</label>
        <div id="input-btn-wrapper">
            <input id="input-txt" type="text" bind:value={prompt} placeholder="Message n0gpt"/>
            <button id="input-btn" type="submit">-</button>
        </div>
    </form>
    
    {#if loading}
        <p>loading...</p>
    {/if}
    {#if !loading}
        <p>{msgResp}</p>
    {/if}
</div>

<style>
    #input-btn-wrapper {
        background-color: purple;
        width: fit-content;
        height: fit-content;
        padding: 10px;
    }
    #input-btn {
        background-color: rgba(0,0,0,0.0);
        border: 0px;
    }
    #input-txt {
        background-color: rgba(0,0,0,0.0);
        border:0px;
    }
</style>