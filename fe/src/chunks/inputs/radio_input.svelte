<script lang="ts">
  // svelte
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  // types
  type TselectedInputColor = { male: string; female: string };
  type TselectedInput = { male: boolean; female: boolean };
  type TinputValues = { first: string; second: string };

  //props
  export let value: TinputValues = { first: "", second: "" };
  export let label: string = "";
  export let valueLabel: TinputValues = { first: "", second: "" };
  export const action: MouseEvent | null = null;

  // states
  let selectedInput: TselectedInput = {
    male: false,
    female: false,
  };
  let selectedGenderColor: TselectedInputColor = {
    male: "",
    female: "",
  };

  // -------- handle the gender choice
  const handleGenderChoice = (gender: number) => {
    gender === 1
      ? ((selectedGenderColor = { male: "selected", female: "" }),
        (selectedInput = { male: true, female: false }))
      : ((selectedGenderColor = { male: "", female: "selected" }),
        (selectedInput = { male: false, female: true }));

    dispatch("action", { option: gender });
  };
</script>

<!-------------- hidden input --------------->
<div class="input-wrapper">
  <input
    type="radio"
    id="gender"
    name="gander"
    value={value.first}
    checked={selectedInput.male}
  />
  <input
    type="radio"
    id="gender"
    name="gander"
    value={value.second}
    checked={selectedInput.female}
  />
</div>

<!-------------- Visible input--------------->
<div
  class="input-interface-wrapper std-flex-justify-start std-flex-align-end std-flex-nowrap"
>
  {#if label}
    <p class="gender-option-label">{label}:</p>
  {/if}

  <!-------------- male gender option --------------->
  <div class="gender-option" on:click={() => handleGenderChoice(1)}>
    <span class="std-bkg std-icon option-selected {selectedGenderColor.male}" />
    <p class="option-letter {selectedGenderColor.male}">{valueLabel.first}</p>
    <div class="svg-wrapper">
      <svg>
        <path
          d="M3 5.7072C50.1565 5.7072 97.3247 5.92723 144.48 5.64704C193.917 5.3533 243.309 3.75524 292.749 3.51136C312.837 3.41227 332.909 3 353 3"
          stroke="#5B7FFF"
          stroke-width="3"
          stroke-linecap="round"
        />
      </svg>
    </div>
  </div>

  <!-------------- female gender option --------------->
  <div class="gender-option" on:click={() => handleGenderChoice(2)}>
    <span
      class="std-bkg std-icon option-selected {selectedGenderColor.female}"
    />
    <p class="option-letter {selectedGenderColor.female}">
      {valueLabel.second}
    </p>
    <div class="svg-wrapper">
      <svg>
        <path
          d="M3 5.7072C50.1565 5.7072 97.3247 5.92723 144.48 5.64704C193.917 5.3533 243.309 3.75524 292.749 3.51136C312.837 3.41227 332.909 3 353 3"
          stroke="#5B7FFF"
          stroke-width="3"
          stroke-linecap="round"
          width="100%"
          height="100%"
        />
      </svg>
    </div>
  </div>
</div>

<style>
  .input-wrapper {
    width: 100%;
    display: none;
    height: 5rem;
  }

  /* -------- visisble wrapper --------- */
  .input-interface-wrapper {
    width: 100%;
    margin: var(--medium-spacing) auto;
  }

  .gender-option-label {
    text-align: left;
    margin: 0;
    width: 30%;
  }

  /* --------- gender option -------- */
  .gender-option {
    margin: 0 var(--medium-spacing) 0 var(--xsmall-spacing);
    position: relative;
    width: 30%;
    cursor: pointer;
  }

  .svg-wrapper {
    position: absolute;
    width: 100%;
    bottom: 0.5rem;
    left: 0;
    width: 5rem;
    height: 1rem;
    padding: 0;
  }
  .svg-wrapper svg {
    width: 100%;
    height: 100%;
  }

  /* ----- seclection "X" icon  -------*/
  .option-selected {
    position: absolute;
    bottom: 0;
    left: 0;
    background-size: contain;
    background-image: url("images/icons/check_x.png");
    display: none;
  }

  .option-selected.selected {
    display: block;
  }
  /* ----------- option letter ------- */
  .option-letter {
    font-size: 2.5rem;
    margin: 0;
    text-align: right;
    width: 5rem;
    color: var(--secondary-color);
  }

  .option-letter:hover {
    color: var(--primary-color);
  }

  .option-letter.selected {
    color: var(--primary-color);
  }
</style>
