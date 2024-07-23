<script>
  import { v4 as uuid } from 'uuid';

  let RTGPositions = ['QB', 'RB', 'WR', 'MLB', 'CB'];
  let archetypes = {
    QB: ['Field General', 'Scrambler', 'Improviser'],
    RB: ['Power Back', 'Elusive Back', 'Receiving Bach'],
    WR: ['Deep Threat', 'Physical', 'Route Runner'],
    MLB: ['Field General', 'Pass Coverage', 'Run Stopper'],
    CB: ['Slot', 'Man-to-Man', 'Zone'],
  };

  export let player;

  let firstName = '';
  let lastName = '';
  let position = '';
  let archetype = '';
  let starRating = 1;
  let hometown = '';
  let startingOverall = 0;
  let draftRound = -1;

  let id = uuid();

  function addPlayer() {
    // TODO - Logic to add player
    let newPlayer = {
      id,
      firstName,
      lastName,
      position,
      archetype,
      starRating,
      hometown,
      startingOverall,
      draftRound,
    };
    players = [...players, newPlayer];
  }
</script>

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
  <select bind:value={archetype} placeholder="Archetype">
    {#each archetypes as a}
      {#if position = a}
      <option value={pos}>
        {pos}
      </option>
    {/each}
  </select>
  <input bind:value={starRating} type="number" placeholder="Star Rating" />
  <input bind:value={hometown} placeholder="Hometown" />
  <input bind:value={startingOverall} type="number" placeholder="Starting Overall" />
  <input bind:value={draftRound} type="number" placeholder="Draft Round" />
  <button on:click={addPlayer}>Add Player</button>
</form>