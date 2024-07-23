<script>
  import { v4 as uuid } from 'uuid';
  import { Button, Modal } from 'flowbite-svelte';
  import Player from '../components/Player.svelte';
  import { players } from '../components/stores.js';

  let formModalOpen = false;
  let playerModalOpen = false;
  let playerStatsModalOpen = false;

  let RTGPositions = ['QB', 'RB', 'WR', 'MLB', 'CB'];

  let firstName = '';
  let lastName = '';
  let position = 'QB';
  let starRating = 1;
  let stats = [];
  let id = uuid();

  function addPlayer() {
    const newPlayer = {
      id,
      firstName,
      lastName,
      position,
      stats,
      starRating
    }
    players.update(currentPlayers => [...currentPlayers, newPlayer]);
    firstName = '';
    lastName = '';
    position = '';
    starRating = 1;
    id = uuid();
  }
  function deletePlayer(id) {
    console.log(id);
    players.set(Object.values($players).filter(p => p.id !== id));
  }
</script>

<main>
  <h1>Road to Glory Players</h1>

  {#each $players as player}
    <div class="player-card" on:click={() => (playerModalOpen = true)}>
      <Player {player} />
      <button class="delete-button" on:click={() => deletePlayer(player.id)}>Delete Player</button>
    </div>
    <Modal title="More Player Info" bind:open={playerModalOpen} outsideclose>
      <!-- TODO: Make this its own component -->
      <h4>{player.firstName}</h4>
      <h3>{player.lastName}</h3>
      <p>{player.position}</p>
    </Modal>
  {/each}

  <!-- Form to add new RTG player -->
  <Button on:click={() => (formModalOpen = true)}>Add New Player</Button>
  <Modal title="Add New Player" bind:open={formModalOpen} autoclose outsideclose>
    <form on:submit|preventDefault={addPlayer}>
      <input bind:value={firstName} placeholder="First Name" />
      <input bind:value={lastName} placeholder="Last Name" />
      <select bind:value={position} placeholder="Position">
        {#each RTGPositions as pos}
          <option value={pos}>
            {pos}
          </option>
        {/each}
      </select>
      <div class="row">
        <p>Star Rating: </p>
        <input bind:value={starRating} type="number" placeholder="Star Rating" />
      </div>
      <button class="add-button" type="submit">Add Player</button>
    </form>
  </Modal>
</main>

<style>
  main {
    padding: 20px;
    max-width: 600px;
    margin: 0 auto;
  }

  form {
    display: flex;
    flex-direction: column;
    gap: 5px;
    margin-bottom: 20px;
  }

  input {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

  button {
    padding: 10px;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .row {
    display: inline-block;
  }

  .add-button {
    background-color: #007BFF;
  }

  .add-button:hover {
    background-color: #0056b3;
  }

  .delete-button {
    background-color: red;
  }

  .delete-button:hover {
    background-color: #8B0000;
  }

  .player-card {
    border: 1px solid #ddd;
    padding: 5px;
    margin-bottom: 10px;
    border-radius: 5px;
    justify-content: left;
  }

</style>