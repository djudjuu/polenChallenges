<script>
  import ChallengeItem from './ChallengeItem.svelte';
  export let challenges;
  export let toggleCompletion;
  export let incrementProgress;
  export let deleteChallenge;
</script>

<ul>
  {#each challenges as challenge, index}
    <ChallengeItem
      {challenge}
      {index}
      {toggleCompletion}
      {incrementProgress}
      {deleteChallenge}
    />
  {/each}
</ul>