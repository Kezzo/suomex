<script lang="ts">
  let currentVocab = $state("sopimus");
  let answerInput = $state("");

  let showingCorrect = $state(false);
  let showingWrong = $state(false);
  let solution = $state("");
  let showingSolution = $state(false);

  function checkAnswer() {
    if (showingCorrect || showingWrong) {
      console.log("next word");
      currentVocab = "viesti";
      showingCorrect = false;
      showingWrong = false;
      answerInput = "";
      solution = "";
      return;
    }

    if (answerInput === "") {
      return;
    }

    if (answerInput.toLowerCase() === "agreement") {
      console.log("correct");
      showingCorrect = true;
    } else {
      showingWrong = true;
    }
  }

  function showSolution() {
    showingSolution = true;
    solution = "agreement";
  }
</script>

<section id="topbar">
  <h2>🇫🇮 Suomex</h2>
</section>

<section id="center">
  <h2>{currentVocab}</h2>
  <div id="answer-input">
    <form
      onsubmit={(e) => {
        e.preventDefault();
        checkAnswer();
      }}
    >
      <input
        type="text"
        bind:value={answerInput}
        readonly={showingCorrect || showingWrong}
        placeholder="kirjoita vastaus.."
      />
    </form>
    <button onclick={checkAnswer}>➡</button>
  </div>
  <h3 hidden={!showingCorrect}>✅ Correct!</h3>

  <div hidden={!showingWrong}>
    <h3>🚫 Wrong!</h3>
    <button onclick={showSolution}>Show Solution</button>
    <h2 hidden={!showingSolution}>{solution}</h2>
  </div>
</section>

<section id="spacer"></section>
