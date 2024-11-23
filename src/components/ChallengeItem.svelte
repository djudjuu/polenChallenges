<script>
  export let challenge;
  export let index;
  export let toggleCompletion;
  export let incrementProgress;
  export let deleteChallenge;
  let progressAmount = 1;
</script>

<li>
  <p><strong>{challenge.description}</strong></p>
  <p>Participants: {challenge.participants.join(", ")}</p>
  <p>Status: <span style="color: {challenge.completed ? 'green' : 'inherit'}">{challenge.completed ? "Completed" : "Incomplete"}</span></p>
  <p>Progress: {challenge.progress} / {challenge.target}</p>
  
  {#if challenge.target === 1}
    <button on:click={() => toggleCompletion(index)}>
      {challenge.completed ? "Completed" : "Complete"}
    </button>
  {:else}
    <input
      type="number"
      bind:value={progressAmount}
      min="1"
      placeholder="Progress amount"
    />
    <button on:click={() => incrementProgress(index, progressAmount)}>Add Progress</button>
  {/if}
  
  <button on:click={() => deleteChallenge(index)}>Delete</button>
</li>