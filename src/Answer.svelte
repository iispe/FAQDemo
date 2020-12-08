<script>
  import { fade } from "svelte/transition";
  import { createEventDispatcher } from "svelte";
  export let answer;
  export let data;

  let dispatch = createEventDispatcher();

  let handlePrioClick = (item) => {
    dispatch("bumpPrio", item.id);

    // item.prio += 1;
    // questionsAsked = [...questionsAsked];
  };
</script>

<style>
  p {
    padding: 1em 0.5em 1em 3em;
    margin: 0;
    background-color: #eee;
    border-radius: 3px;
    box-shadow: 0px 3px 4px rgba(0, 0, 0, 0.2);
    display: flex;
    justify-content: space-between;
  }
  .answer {
    font-weight: 500;
  }
  #upvote {
    font-weight: 300;
    cursor: pointer;
    min-width: 50px;
  }
</style>

<p class="answer" in:fade on:click|once={() => handlePrioClick(data)}>
  {answer}
  <span id="upvote">(+) {data.prio}</span>
</p>
