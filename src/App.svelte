<script lang="ts">
  import Cowboy from './lib/Cowboy.svelte';
  import Sun from './lib/Sun.svelte';
  let player1 : Cowboy
  let player2 : Cowboy


  function fire() {
    player1.shoot()
    player2.shoot()
  }
  function shoot() {
    player1.shoot()
    player2.die()
  }
  function die() {
    player1.die()
    player2.die()
  }
  function reload() {
    player1.reload()
    player2.reload()
  }
</script>

<main>
  <h1>Cowboy</h1>
  <button on:click={fire}>Fire</button>
  <button on:click={shoot}>Shoot</button>
  <button on:click={die}>Die</button>
  <button on:click={reload}>Reload</button>
  <Sun/>
    <div class="floor">
      <div class="player">
        <Cowboy bind:this={player1}/>
        <Cowboy bind:this={player2} reverse={true} skinID={1}/>
      </div>

    </div>
</main>

<style>
  .floor {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 45vh;
    background-color: rgb(114, 78, 38);
  }
  .floor:before{
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    top:-.5em;
    background-image: url("/floor.png");
    background-size: auto 1em;
    height: 1em;
    font-size: 30px;
    background-position-x: center;
    image-rendering: pixelated;
}
  .player {
    display: flex;
    justify-content: space-between;
    position: absolute;
    font-size: 50px;
    left: 2em;
    right: 2em;
    bottom: 100%;
    margin-bottom: -60px;
  }
</style>
