<script>
  // Reactive variables for challenges and form inputs
  let challenges = [
    {
      description: "Eisbaden",
      participants: ["Antonk", "Conrad"],
      completed: false
    },
    {
      description: "300 bahnen pro tag",
      participants: ["alle"],
      completed: false
    },
	];
  let description = "";
  let participants = "";

  // Add a new challenge
  function addChallenge() {
    if (description.trim()) {
      challenges = [
        ...challenges,
        {
          description,
          participants: participants.split(",").map(p => p.trim()),
          completed: false
        }
      ];
      description = "";
      participants = "";
    }
  }

  // Toggle challenge completion
  function toggleCompletion(index) {
    challenges[index].completed = !challenges[index].completed;
  }

  // add a function to remove a challenge
  function deleteChallenge(index) {
	challenges = challenges.filter((_, i) => i !== index);
  }
</script>

<main>
  <h1>Vacation Challenge List</h1>

  <!-- Add Challenge Form -->
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
    <button on:click={addChallenge}>Add Challenge</button>
  </div>

  <!-- Display Challenges -->
  <ul>
    {#each challenges as challenge, index}
      <li>
        <p><strong>{challenge.description}</strong></p>
        <p>Participants: {challenge.participants.join(", ")}</p>
        <p>Status: {challenge.completed ? "Completed" : "Incomplete"}</p>
        <button on:click={() => toggleCompletion(index)}>
          {challenge.completed ? "Undo" : "Complete"}
        </button>
        <button on:click={() => deleteChallenge(index)}>Delete</button>
      </li>
    {/each}
  </ul>
</main>

<style>
  main {
    font-family: Arial, sans-serif;
    padding: 1rem;
    max-width: 600px;
    margin: auto;
  }

  input {
    margin: 0.5rem;
    padding: 0.5rem;
    font-size: 1rem;
  }

  button {
    margin: 0.5rem;
    padding: 0.5rem 1rem;
    font-size: 1rem;
  }

  li {
    margin: 1rem 0;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  li p {
    margin: 0.5rem 0;
  }
</style>
