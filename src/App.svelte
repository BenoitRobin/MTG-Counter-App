<script>
  import Team from "./Team.svelte";

  let blueScore = 20;
  let redScore = 20;

  $: redWon = blueScore === 0;
  $: blueWon = redScore === 0;
  $: gameOver = redWon || blueWon;

  function newGame() {
    redScore = 20;
    blueScore = 20;
  }
</script>

<div class="row mt-2">
  <div class="col">
    <h1 class="text-center">MTG Counter APP</h1>
  </div>
</div>

<div class="row">
  <Team {gameOver} team="Red" bind:score={redScore} />
  <Team {gameOver} team="Blue" bind:score={blueScore} />
</div>

{#if !gameOver}
  <div class="row">
    <button on:click={newGame} class="btn btn-warning mt-5 mx-auto w-50"
      >Reset Game</button
    >
  </div>
{:else}
  {#if blueWon}
    <h2 class="text-center">Bravo Blue!</h2>
  {:else}
    <h2 class="text-center">Bravo Red!</h2>
  {/if}
  <div class="row">
    <button on:click={newGame} class="btn btn-success mt-5 mx-auto w-50"
      >New Game</button
    >
  </div>
{/if}
