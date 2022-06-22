<header>
    <h1>Let's Play Tic Tac Toe!</h1>
    <small>* made with Svelte</small>
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
    margin: 2rem auto 0;
    max-width: 14rem;
  }

  small {
    color: #ff3e00;
    font-weight: 700;
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