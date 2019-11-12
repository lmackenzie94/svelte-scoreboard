<script>
  import Navbar from "./Navbar.svelte";
  import Player from "./Player.svelte";
  import AddPlayer from "./AddPlayer.svelte";
  import { storedPlayers } from "./stores.js";
  import { onMount, onDestroy } from "svelte";

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
  const addPlayer = e => {
    // we get the event data with e.detail
    const newPlayer = e.detail;
    // can't do this:
    // players.push(newPlayer); // won't be reactive (like in React you can't just push to state)
    // this assignment (=) triggers the reactivity
    initialPlayers = [...initialPlayers, newPlayer];
  };

  const deletePlayer = e => {
    const playerToDelete = e.detail;
    initialPlayers = initialPlayers.filter(
      player => player.name !== playerToDelete
    );
  };

  onMount(() => {
    storedPlayers.set(initialPlayers);
  });

  const unsubscribe = storedPlayers.subscribe(value => {
    initialPlayers = value;
  });
  onDestroy(unsubscribe);

  console.log(storedPlayers);
</script>

<Navbar />
<div class="container">
  <AddPlayer />
  {#if initialPlayers.length === 0}
    <p>No Players</p>
  {:else}
    {#each initialPlayers as player}
      <Player
        name={player.name}
        points={player.points}
        on:deleteplayer={deletePlayer} />
    {/each}
  {/if}
</div>
