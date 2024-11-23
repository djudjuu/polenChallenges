<script>
  export let challenge;
  export let index;
  export let toggleCompletion;
  export let incrementProgress;
  export let deleteChallenge;
  let progressAmount = 1;
</script>

<li class:completed={challenge.completed}>
  <p><strong>{challenge.description}</strong></p>
  <p>Participants: {challenge.participants.join(", ")}</p>
  <p>Status: <span style="color: {challenge.completed ? 'green' : 'inherit'}">{challenge.completed ? "Completed" : "Incomplete"}</span></p>
  
  {#if challenge.target === 1 && !challenge.completed}
    <button on:click={() => toggleCompletion(index)}>
      {challenge.completed ? "Completed" : "Complete"}
    </button>
  {:else if !challenge.completed}
    <p>Progress: {challenge.progress} / {challenge.target}</p>
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

<style>
  li {
    border: 2px solid #4b4b8f; /* Default border color */
    padding: 10px;
    margin: 10px 0;
    border-radius: 5px;
    background-color: #4b4b8f; /* Vaporwave medium purple */
  }

  li.completed {
    border-color: #39ff14; /* Neon green border color when completed */
  }
</style>