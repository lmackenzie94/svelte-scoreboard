<script>
  import Navbar from "./Navbar.svelte";
  import Player from "./Player.svelte";
  import AddPlayer from "./AddPlayer.svelte";
  import { storedPlayers } from "./stores.js";
  import { onMount } from "svelte";

  // variables
  let name = "Luke";
  let points = 100;
  let showControls = false;
  let initialPlayers = [
    {
      name: "Luke MacKenzie",
      points: 69
    },
    {
      name: "John Doe",
      points: 47
    }
  ];

  // functions
  const addPoint = () => (points += 1);
  const removePoint = () => (points -= 1);
  const toggleControls = () => (showControls = !showControls);

  // set initial players
  onMount(() => {
    storedPlayers.set(initialPlayers);
  });
</script>

<Navbar />
<div class="container">
  <AddPlayer />
  {#if $storedPlayers.length === 0}
    <p>No Players</p>
  {:else}
    {#each $storedPlayers as player}
      <Player name={player.name} points={player.points} />
    {/each}
  {/if}
</div>
