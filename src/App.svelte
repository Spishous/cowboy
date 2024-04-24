<script lang="ts">
  import Cowboy from './lib/Cowboy.svelte';
</script>

<main>
  <h1>Cowboy</h1>
    <div class="floor">
      <div class="player">
        <Cowboy />
        <Cowboy reverse={true} />
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
