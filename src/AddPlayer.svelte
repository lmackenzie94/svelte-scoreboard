<script>
  import { storedPlayers } from "./stores.js";

  let player = {
    name: "",
    points: 0
  };

  const onSubmit = () => {
    storedPlayers.update(existing => {
      let allPlayers = [...existing, player];
      return allPlayers;
    });
  };
</script>

<form on:submit|preventDefault={onSubmit} class="grid-3">
  <input type="text" placeholder="Player Name" bind:value={player.name} />
  <input type="number" placeholder="Player Name" bind:value={player.points} />
  <input type="submit" value="Add Player" class="btn btn-primary" />
</form>
