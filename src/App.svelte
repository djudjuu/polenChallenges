<script>
// Reactive variables for challenges and form inputs
  let challenges = [
    {
      description: "Eisbaden",
      participants: ["Alice", "Bob"],
      completed: false
    },
    {
      description: "Read a book",
      participants: ["Charlie"],
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

  // Add a function to remove a challenge
  function deleteChallenge(index) {
    challenges = challenges.filter((_, i) => i !== index);
  }
</script>

<main>
  <h1 class="flashy-heading">
    Vacation Challenge List
  </h1>
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
  @keyframes blink {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0;
    }
  }

  .flashy-heading {
    color: #ff77ff; /* Vaporwave pink */
    text-shadow: 2px 2px 4px #00ffff; /* Vaporwave cyan */
    font-size: 3em;
    text-align: center;
    margin-top: 20px;
    animation: blink 1s infinite;
  }

  main {
    font-family: 'Comic Sans MS', cursive, sans-serif;
    background-color: #2e2b5f; /* Vaporwave dark purple */
    color: #ffffff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  }

  input, button {
    margin: 5px;
    padding: 10px;
    border-radius: 5px;
    border: none;
    font-size: 1em;
  }

  button {
    background-color: #ff77ff; /* Vaporwave pink */
    color: #2e2b5f; /* Vaporwave dark purple */
    cursor: pointer;
  }

  button:hover {
    background-color: #00ffff; /* Vaporwave cyan */
    color: #2e2b5f; /* Vaporwave dark purple */
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    background-color: #4b4b8f; /* Vaporwave medium purple */
    margin: 10px 0;
    padding: 10px;
    border-radius: 5px;
  }

  li p {
    margin: 5px 0;
  }
</style>