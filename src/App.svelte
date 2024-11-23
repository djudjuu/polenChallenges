<script>
  import AddChallengeForm from './components/AddChallengeForm.svelte';
  import ChallengeList from './components/ChallengeList.svelte';

  let challenges = [
    {
      description: "Go hiking",
      participants: ["Alice", "Bob"],
      completed: false,
      target: 1,
      progress: 0
    },
    {
      description: "Read a book",
      participants: ["Charlie"],
      completed: false,
      target: 1,
      progress: 0
    },
    {
      description: "Swim 300 laps",
      participants: ["Alice", "Charlie"],
      completed: false,
      target: 300,
      progress: 0
    }
  ];
  let description = "";
  let participants = "";
  let target = 1;

  function addChallenge() {
    if (description.trim()) {
      challenges = [
        ...challenges,
        {
          description,
          participants: participants.split(",").map(p => p.trim()),
          completed: false,
          target,
          progress: 0
        }
      ];
      description = "";
      participants = "";
      target = 1;
    }
  }

  function toggleCompletion(index) {
    challenges[index].completed = !challenges[index].completed;
  }

  function incrementProgress(index, amount) {
    if (!challenges[index].completed) {
      challenges[index].progress += amount || 1;
      if (challenges[index].progress >= challenges[index].target) {
        challenges[index].completed = true;
      }
    }
  }

  function deleteChallenge(index) {
    challenges = challenges.filter((_, i) => i !== index);
  }
</script>

<main>
  <h1 class="flashy-heading">Vacation Challenge List</h1>
  <AddChallengeForm
    bind:description={description}
    bind:participants={participants}
    bind:target={target}
    {addChallenge}
  />
  <ChallengeList
    {challenges}
    {toggleCompletion}
    {incrementProgress}
    {deleteChallenge}
  />
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