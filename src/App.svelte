<script>
  import { onMount } from "svelte";

  const minNum = 0;
  const maxNum = 100;
  let answer;
  let attempts = 0;
  let guess = "";
  let message = "";
  let gameOver = false;

  onMount(() => {
    answer = Math.floor(Math.random() * (maxNum - minNum + 1)) + minNum;
  });

  function handelGuess() {
    const guessNum = Number(guess);

    if (isNaN(guessNum) || guessNum < minNum || guessNum > maxNum) {
      message = "Are you shure? if not; Please enter a valid number";
    } else {
      attempts++;

      if (guessNum < answer) {
        message = "Too low, try a higher number.";
      } else if (guessNum > answer) {
        message = "Too high, try a smaller number";
      } else {
        message = `You are correct, Good guess ${answer}. Your number of attempts ${attempts}” `;
        gameOver = true;
      }
    }
    guess = "";
  }

  function resetGame() {
    answer = Math.floor(Math.random() * (maxNum - minNum + 1)) + minNum;
    attempts = 0;
    guess = "";
    message = "";
    gameOver = false;
  }
</script>

<main>
  <h1>Guess number between 1-100</h1>
  <p>Input guess here.</p>

  {#if !gameOver}
    <input
      type="number"
      bind:value={guess}
      min={minNum}
      max={maxNum}
      placeholder="Enter your guess"
    />
    <button on:click={handelGuess}>Submit Guess</button>
  {:else}
    <button on:click={resetGame}>Play Again</button>
  {/if}

  {#if message}
    <p>{message}</p>
  {/if}
</main>

<style>
  main {
    background-color: rgb(37, 37, 37);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    text-align: center;
    padding: 1em;
    min-width: 100vh;
    min-height: 100vh;
    margin: 0;
  }

  h1 {
    color: rgb(197, 17, 17);
    font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 125;
  }

  input {
    width: 125px;
  }

  p {
    color: rgb(204, 167, 167);
    font-size: 1.5rem;
  }

  button {
    color: rgb(204, 167, 167);
  }

  @media (min-width: 100vh) {
    main {
      max-width: none;
    }
  }
</style>
