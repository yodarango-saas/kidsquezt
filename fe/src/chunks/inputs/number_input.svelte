<script lang="ts">
  // states
  let currAge: string = "age";
  let ageDPdisplay: string = "";
  // ---------- check the input is a number
  const handleSelectAge = (age: number) => {
    currAge = age.toString();
    ageDPdisplay = "";
  };
</script>

<div
  class="main-wrapper"
  onclick={(e) => (ageDPdisplay = "age-dropdown-display")}
>
  <div class="input-wrapper">
    <!-- hidden input -->
    <input
      type="number"
      maxlength="3"
      class="std-input hidden"
      placeholder=""
      required
    />

    <!---------- age dropdown --------->
    <div class="age-dropdown {ageDPdisplay}">
      {#each new Array(15) as age, i}
        <p class="std-flex-row" onclick={() => handleSelectAge(i + 1)}>
          {i + 1}
        </p>
      {/each}
    </div>

    <!---------- current age --------->
    <p class="std-input currAge">
      {currAge}
    </p>

    <!---------- svg wrapper --------->
    <div class="svg-wrapper">
      <svg viewBox="0 0 356 9">
        <path
          d="M3 5.7072C50.1565 5.7072 97.3247 5.92723 144.48 5.64704C193.917 5.3533 243.309 3.75524 292.749 3.51136C312.837 3.41227 332.909 3 353 3"
          stroke="#5B7FFF"
          stroke-width="20"
          stroke-linecap="round"
        />
      </svg>
    </div>
  </div>
</div>

<style>
  .main-wrapper {
    width: 50%;
  }
  .input-wrapper {
    margin: var(--medium-spacing) 0;
    width: 100%;
    height: 2rem;
    position: relative;
  }

  .input-wrapper input {
    display: none;
    margin: 0;
  }

  .svg-wrapper {
    width: 100%;
    margin: 0;
  }

  .svg-wrapper svg {
    width: 100%;
  }

  .currAge {
    width: 100%;
    height: 100%;
    color: var(--secondary-color);
    margin: 0;
    text-align: left;
  }

  .age-dropdown {
    display: none;
    width: 100%;
    height: 20rem;
    position: absolute;
    overflow-y: scroll;
    background-color: var(--accent-color);
    border-radius: 1rem;
  }

  .age-dropdown:hover {
    cursor: pointer;
  }

  .age-dropdown p {
    margin: 0;
    height: 5rem;
    border-bottom: 0.2rem solid #f2f2f2;
  }

  .age-dropdown p:hover {
    background-color: #f2f2f2;
  }

  .age-dropdown-display {
    display: block;
  }
</style>
