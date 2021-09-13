<script>
    import {fade} from "svelte/transition"
    import {onMount} from "svelte"

    let count = 0
    let visible = false
    let history = []
    let audio

    onMount(() => {
        visible = true
    })

    function reset(){
        if (history.length == 5){
            history.splice(0, 1)
        }
        history = [...history, count]
        count=0
    }
</script>

<audio src="tap.mp3" bind:this={audio} preload="auto"></audio>

{#if visible}
    <div transition:fade="{{duration:750}}" class="container">
        <div class="row center-align green-text count-number-row">
            <div class="col s12 m12 l12">
                <span class="count-number">{count}</span>
            </div>
        </div>
        <div class="row">
            <div class="col s12 m12 l12 center-align">
                <button on:click={()=>{count++; audio.play()}} class="btn green white-text waves-effect waves-light">
                    <span class="btn-text">+</span></button>
            </div>
            <div class="col s12 m12 l12 center-align grey-text reset-link-container">
                <span class="reset-link" on:click={reset}>Сбросить</span>
            </div>
        </div>
        <div class="row">
            <div class="col s12 m12 l12">
                {#if history.length != 0}
                    <ul class="collection">
                        {#each history as point}
                            <li transition:fade class="collection-item">{point}</li>
                        {/each}
                    </ul>
                {/if}
            </div>
        </div>

    </div>
{/if}

<style>
    .count-number {
        font-size: 64px;
        font-weight: bold;
    }

    .count-number-row {
        margin-top: 10%;
    }

    button {
        font-size: 128px;
        height: 200px;
        width: 200px;
        justify-content: center;
        border-radius: 50%;
        align-items: center;
        display: flex;
        margin: auto;
        margin-top: 50px;
    }

    .btn-text {
        margin-top: -28px;
    }

    .reset-link-container {
        margin-top: 25px;
    }

    .reset-link {
        font-weight: bold;
        cursor: pointer;
        font-size: 18px;
        user-select: none;
    }
</style>