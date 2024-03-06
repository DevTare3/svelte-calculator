<script>
  let numberOne = 1;
  let numberTwo = 1;
  let numberThree = 1;
  let isFalseOne = false;
  let isFalseTwo = false;
  let isFalseThree = false;
  let days = "--";
  let months = "--";
  let years = "--";
  const date = new Date();
  function getDay(year, month) {
    return new Date(year, month, 0).getDate();
  }
  function allowedKeys(event) {
    const keys = [
      "1",
      "2",
      "3",
      "4",
      "5",
      "6",
      "7",
      "8",
      "9",
      "Backspace",
      "Tab",
    ];
    if (!keys.includes(event.key)) event.preventDefault();
  }
  function handleClick(e) {
    let yearChange = false;
    months = date.getMonth() + 1 - numberTwo;
    if (months < 0) {
      months += 12;
      yearChange = true;
    }
    years = date.getFullYear() - numberThree;
    if (yearChange) years--;
    days = date.getDate() - numberOne;
    if (days < 0) {
      months--;
      days += getDay(years, months);
    }
  }

  $: {
    if (numberOne <= 0 || numberOne > getDay(numberThree, numberTwo)) {
      numberOne = numberOne;
      isFalseOne = true;
    } else isFalseOne = false;

    if (numberTwo > 12 || numberTwo <= 0) {
      numberTwo = numberTwo;
      isFalseTwo = true;
    } else isFalseTwo = false;

    if (numberThree > date.getFullYear() || numberThree <= 0) {
      numberThree = numberThree;
      isFalseThree = true;
    } else isFalseThree = false;
    if (isFalseOne) {
    }
  }
</script>

<main>
  <article>
    <div class="flex">
      <div>
        <p class="small" class:redLetter={isFalseOne}>Day</p>
        <input
          type="text"
          bind:value={numberOne}
          placeholder="DD"
          on:keydown={allowedKeys}
          class:error={numberOne <= 0 ||
            numberOne > getDay(numberThree, numberTwo)}
        />
        {#if isFalseOne}
          <p class="error-text one">This field is requiered</p>
        {/if}
      </div>
      <div>
        <p class="small" class:redLetter={isFalseTwo}>Month</p>
        <input
          type="text"
          bind:value={numberTwo}
          placeholder="MM"
          on:keydown={allowedKeys}
          class:error={numberTwo > 12 || numberTwo <= 0}
        />
        {#if isFalseTwo}
          <p class="error-text two">This field is requiered</p>
        {/if}
      </div>
      <div>
        <p class="small" class:redLetter={isFalseThree}>Year</p>
        <input
          type="text"
          bind:value={numberThree}
          placeholder="YYYY"
          on:keydown={allowedKeys}
          class:error={numberThree > date.getFullYear() || numberThree <= 0}
        />
        {#if isFalseThree}
          <p class="error-text three">This field is requiered</p>
        {/if}
      </div>
      <input
        tabindex="0"
        type="submit"
        class="press"
        value=""
        on:click={handleClick}
      />
    </div>
    <p class="big"><span class="years">{years} </span>years</p>
    <p class="big"><span class="months">{months} </span>months</p>
    <p class="big"><span class="days">{days} </span>days</p>
  </article>
</main>

<!-- <div class="attribution" style="display: none;">
  Challenge by <a
    href="https://www.frontendmentor.io?ref=challenge"
    target="_blank">Frontend Mentor</a
  >. Coded by <a href="https://twitter.com/mujezinovicbiz">DevTare</a>.
</div> -->

<style>
  .error {
    border: 2px solid red;
  }
  .redLetter.redLetter {
    color: red;
  }
  main {
    background-color: var(--Off-white);
    margin: 0 auto;
    padding-inline: min(90vw, 1rem);
    position: relative;
    height: 100vh;
  }
  article {
    background-color: var(--White);
    padding-block: min(2.5rem, 6vw);
    padding-inline: min(2.5rem, 4vw);
    border-radius: 2rem 2rem 5rem 2rem;
    width: clamp(5rem, 60vw, 60rem);
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 25%;
    right: 25%;
  }
  div > input {
    position: relative;
  }
  .small {
    font-family: var(--Poppins);
    letter-spacing: 0.125em;
    font-weight: 700;
    margin-block-end: min(0.3em, 2vw);
    font-size: min(1em, 2vw);
    text-transform: uppercase;
    color: var(--Smokey-grey);
    position: relative;
  }
  .error-text {
    color: red;
    font-size: min(0.8rem, 1.3vw);
    font-weight: 400;
    text-transform: none;
    min-width: 40ch;
    position: absolute;
    top: 80%;
  }
  .flex {
    position: relative;
    display: flex;
    gap: min(2rem, 5vw);
    border-bottom: 1px solid var(--Light-grey);
  }
  input {
    border-radius: 0.5em;
    border: 1px solid var(--Light-grey);
    font-family: var(--Poppins);
    font-weight: var(--poppins-800);
    font-size: min(1.3em, 2.5vw);
    padding-block: min(1em, 2vw);
    padding-inline: min(1em, 2vw);
    width: min(10rem, 14vw);
    cursor: pointer;
    outline: none;
    margin-bottom: min(2em, 15vw);
  }
  input::placeholder {
    font-size: min(1.2em, 2.5vw);
  }

  .big {
    font-family: var(--Poppins);
    font-weight: var(--poppins-800);
    font-style: italic;
    font-size: min(5em, 6vw);
    color: black;
  }
  span {
    color: var(--Purple);
  }
  .press {
    background-image: url("$lib/images/icon-arrow.svg");
    background-size: min(2.5rem, 4vw);
    background-position: center center;
    background-repeat: no-repeat;
    max-width: 4rem;
    min-height: 1.5rem;
    position: absolute;
    outline: none;
    padding: 1rem;
    border-radius: 50%;
    background-color: var(--Purple);
    border: none;
    cursor: pointer;
    left: 91%;
    top: 79%;
  }
  .press:hover {
    background-color: var(--Off-black);
    transition: ease-in 3ms;
  }
  .press:focus {
    outline: 1px solid red;
    background-color: var(--Off-black);
    transition: ease-in 3ms;
  }

  .big:first-of-type {
    margin-block-start: min(0.5em, 5vw);
  }

  div > p {
    margin-bottom: 2rem;
  }
  @media (max-width: 813px) {
    .press {
      max-width: 2.5rem;
      min-height: 1.5rem;
      top: 80%;
      left: 45%;
    }
  }
  @media (max-width: 390px) {
    .press {
      width: 0.5rem;
      height: 0.5rem;
      top: 75%;
      left: 42%;
    }
  }
</style>
