<script>
  export let player;
</script>

<div>
  <h4>{player.firstName}</h4>
  <h3>{player.lastName}</h3>
  <p>{player.position}</p>
  <p>{player.starRating} ★</p>
</div>

<style>
  .player {
    border: 1px solid #ddd;
    padding: 5px;
    margin-bottom: 10px;
    border-radius: 5px;
    justify-content: left;
  }
  .delete {
    color: white;
    background-color: red;
    justify-content: right;
    margin-bottom: 5px;
  }
</style>