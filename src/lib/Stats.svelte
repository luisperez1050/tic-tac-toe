<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher();
    // default value
    export let nextPlayer = 'X'
    export let winner
    export let score
    export let round = 1
    export let emptySquares


    function newRound() {
        dispatch('round')
    }

</script>

<div class="stats">
    <div class="scores">
        <small>Current Player: {nextPlayer} </small>
        <small>Score: X - {score.X} | O - {score.O} | Tie - {score.Tie}</small>
        <small>Round: {round}</small>
    </div>
    {#if winner || emptySquares === 0}
        <div class="rounds">
            <button on:click={newRound}>Play Another Round</button>
        </div>
    {/if}
</div>

<style>
    small {
        max-width: 800px;
        margin: 0 auto;
    }
    small {
        display: block;
        text-align: left;
    }
    button {
        padding: 10px 14px;
        background-color: #ff3e00;
        color: white;
        font-weight: 700;
        border: none;
        font-size: 20px;
        cursor: pointer;
    }
    button:hover {
        background-color: #c13000;
    }
    .stats {
        max-width: 800px;
        margin: 0 auto;
    }
    .stats div + div {
        margin-left: 20px;
    }
    .scores, .rounds {
        display: inline-block;
        vertical-align: bottom;
    }
</style>
