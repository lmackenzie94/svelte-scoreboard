<script>
  import Navbar from "./Navbar.svelte";
  import Player from "./Player.svelte";
  import AddPlayer from "./AddPlayer.svelte";

  let name = "Luke";
  let points = 100;
  let showControls = false;

  const addPoint = () => (points += 1);
  const removePoint = () => (points -= 1);
  const toggleControls = () => (showControls = !showControls);
  const addPlayer = e => {
    // we get the event data with e.detail
    const newPlayer = e.detail;
    // can't do this:
    // players.push(newPlayer); // won't be reactive (like in React you can't just push to state)
    // this assignment (=) triggers the reactivity
    players = [...players, newPlayer];
  };

  const deletePlayer = e => {
    const playerToDelete = e.detail;
    players = players.filter(player => player.name !== playerToDelete);
  };

  let players = [
    {
      name: "Luke MacKenzie",
      points: 69
    },
    {
      name: "John Doe",
      points: 47
    }
  ];
</script>

<Navbar />
<div class="container">
  <AddPlayer on:addplayer={addPlayer} />
  {#if players.length === 0}
    <p>No Players</p>
  {:else}
    {#each players as player}
      <Player
        name={player.name}
        points={player.points}
        on:deleteplayer={deletePlayer} />
    {/each}
  {/if}
</div>
