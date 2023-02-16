<script>
    import Banner from './Banner.svelte'
    import Stats from './Stats.svelte'

    let turn = '';
    let nextPlayer = turn === 'X' ? 'O' : 'X'
    let winner = null;
    let score = {X: 0, O: 0, Tie: 0}
    let round = 1
    // create an array with default of empty string
    const winningCombinations = [
        [0,1,2],
        [3,4,5],
        [6,7,8],
        [0,4,8],
        [2,4,6],
        [0,3,6],
        [1,4,7],
        [2,5,8]
    ]
    let Ocombinations = [];
    let Xcombinations = [];
    let boardSquares = new Array(9).fill('');
    let emptySquares = boardSquares.filter((square) => square === '')?.length;

    /**
     * @param {number} index
     */
    function selectBlock(index, override = null) {
        turn = turn === 'X' ? 'O' : 'X'
        if (override) turn = override
        if(!winner) nextPlayer = turn === 'X' ? 'O' : 'X'

        boardSquares[index] = turn;
        winner = checkWinner() ?? null;
        emptySquares = boardSquares.filter((square) => square === '')?.length;
        if (winner) tallyScore(winner);
        document.querySelector(`#square_${index}`)?.classList.remove('selectable');
    };
    function checkWinner() {
        Xcombinations = boardSquares.map((square, index) => { if (square === 'X') return index });
        Ocombinations = boardSquares.map((square, index) => { if (square === 'O') return index });
        for (const combinations of winningCombinations) {
            const checkX = combinations.filter((item) => Xcombinations.indexOf(item) !== -1)?.length;
            const checkO = combinations.filter((item) => Ocombinations.indexOf(item) !== -1)?.length;

            if (checkX === 3) return 'X'
            if (checkO === 3) return 'O'
        }
    }
    /**
     * @param {string} player
     */
    function tallyScore(player) {
        score[player]++
    }
    function nextRound() {
        if(!winner) score.Tie++
        round++;
        winner = null;
        turn = '';
        nextPlayer= 'X';
        boardSquares.map((square, index) => boardSquares[index] = '');
        emptySquares = boardSquares.filter((square) => square === '')?.length
        document.querySelectorAll('.square').forEach((square) => square.classList.add('selectable'))
    }
</script>

<Banner winner={winner} emptySquares={emptySquares}/>
<div class="board">
    {#each boardSquares as square, index}
        <div class="square selectable" id="square_{index}" on:click={() => { if (!winner && !square && emptySquares > 0) selectBlock(index) }}>
            {square}
        </div>
    {/each}
</div>

<Stats nextPlayer={nextPlayer} winner={winner} score={score} round={round} emptySquares={emptySquares} on:round={nextRound}/>

<style>
    .board{
        background-color: #ff3e00;
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(3, 100px);
        gap: 15px;
        max-width: 800px;
        margin: 32px auto;
    }
    .square {
        background-color: white;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 70px;
        font-weight: 700;
    }
    .selectable:hover {
        opacity: 0.9;
    }

</style>