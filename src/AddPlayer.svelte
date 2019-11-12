<script>
  import { createEventDispatcher } from "svelte";
  import { storedPlayers } from "./stores.js";

  const dispatch = createEventDispatcher();

  let player = {
    name: "",
    points: 0
  };

  // const onSubmit = () => {
  //   // e.preventDefault(); instead, use preventDefault event modifier
  //   // creating an event 'addplayer' that will dispatch the player data
  //   dispatch("addplayer", player);
  //   // reset
  //   player = {
  //     name: "",
  //     points: 0
  //   };
  // };

  const onSubmit = () => {
    storedPlayers.update(existing => {
      let allPlayers = [...existing, player];
      return allPlayers;
    });
  };
</script>

<!-- <form on:submit={onSubmit} class="grid-3"> BETTER WAY: -->
<form on:submit|preventDefault={onSubmit} class="grid-3">
  <input type="text" placeholder="Player Name" bind:value={player.name} />
  <input type="number" placeholder="Player Name" bind:value={player.points} />
  <input type="submit" value="Add Player" class="btn btn-primary" />
</form>
