<script>
  export let description;
  export let participants;
  export let target;
  export let addChallenge;
</script>

<div>
  <input
    type="text"
    bind:value={description}
    placeholder="Challenge description"
  />
  <input
    type="text"
    bind:value={participants}
    placeholder="Participants (comma-separated)"
  />
  <input
    type="number"
    bind:value={target}
    min="1"
    placeholder="Target (e.g., number of times)"
  />
  <button on:click={addChallenge}>Add Challenge</button>
</div>