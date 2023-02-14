<script>
    export let winner
    export let emptySquares

</script>
<header>
    <h1>Let's Play Tic Tac Toe!</h1>
    <p>
      {#if winner}
          Winner: {winner}
      {:else if emptySquares === 9}
          Please select a spot
      {:else if emptySquares === 0}
          Its a tie, play another round
      {:else}
          Keep Playing {emptySquares} spaces left
      {/if}
    </p>
</header>

<style>
  header {
    max-width: 1000px;
    margin: 0 auto 32px;
    box-shadow: #ff3e00 3px 3px 20px 4px;
    border-radius: 10px;
    padding: 15px 0;
  }

  h1 {
    color: #ff3e00;
    font-size: 3rem;
    font-weight: 100;
    line-height: 1.1;
    margin: auto 0;
    max-width: 14rem;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
</style>