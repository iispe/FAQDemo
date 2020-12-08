<script>
  import Answer from "./Answer.svelte";
  import Search from "./Search.svelte";
  let questionsAsked = [
    {
      id: 1,
      prio: 2,
      question: "Miten tämä osaa näyttää pidemmät vastaukset?",
      answer:
        "Nullam in ante mi. Donec et faucibus ligula. Pellentesque vulputate, risus vitae blandit ultricies, est nisl placerat mi, ac aliquet nunc erat ut leo. Sed semper congue placerat. Phasellus hendrerit mi metus, eget efficitur velit porta sit amet. Cras vitae gravida purus. Nam eu lacinia enim. Maecenas non nibh ipsum.",
      show: false,
    },
    {
      id: 2,
      prio: 3,
      question: "Miten näen vastaukset?",
      answer: "Jos näet tämän, osasit klikata vastauksen auki",
      show: false,
    },
    {
      id: 3,
      prio: 1,
      question: "Ja mikä on tuo mystinen (+) merkki vastauksessa?",
      answer:
        "Jos kokee kysymyksen tärkeäksi, voi plussalla nostaa sitä ylemmäs kysymyslistalla. Vaikuttaa siis kysymys/vastauksen prioriteettiarvoon.",
      show: false,
    },
    {
      id: 4,
      prio: 1,
      question:
        "Olihan tässä hassuja kysymyksiä ja kummallisia vastauksia, mutta tämä onkin demo",
      answer: "Joo, no sillai sitte.",
      show: false,
    },
  ];

  let showAnswer = (item) => {
    item.show = !item.show;
    questionsAsked = [...questionsAsked];
    // if (toggleAnswer === " + ") {
    //   toggleAnswer = " - ";
    // } else {
    //   toggleAnswer = " + ";
    // }
  };

  let buttonText = "Näytä";
  let showSearch = false;
  let toggleAnswer = " + ";

  $: questionsAsked.sort((a, b) =>
    a.prio < b.prio ? 1 : a.prio === b.prio ? (a.id > b.id ? 1 : -1) : -1
  );

  const bumpPrio = (e) => {
    questionsAsked.map((q) => {
      if (q.id === e.detail) {
        q.prio += 1;
      }
    });
    questionsAsked = [...questionsAsked];
  };
</script>

<style>
  .container {
    padding-top: 1em;
    border-top: 1px solid #aaa;
  }
  .question {
    font-weight: 700;
    min-width: 60%;
    align-items: center;
    margin-bottom: 0;
    /* padding-bottom: 0.5em; */
    border-bottom: 1px solid #c1c1c1;
  }
  p {
    cursor: pointer;
  }
  span {
    padding-right: 1em;
  }
</style>

<div class="container">
  {#if showSearch}
    <Search />
  {/if}
  {#each questionsAsked as item}
    <div class="question">
      <p on:click={() => showAnswer(item)}>
        <span>
          {#if item.show}-{:else}+{/if}
        </span>{item.question}
      </p>

      {#if item.show}
        <Answer answer={item.answer} data={item} on:bumpPrio={bumpPrio} />
      {/if}
    </div>
  {/each}
</div>
