<script lang="ts">
  export let isChecked: boolean = false;
</script>

<div class="input-wrapper">
  <input
    type="radio"
    id="gender"
    name="gander"
    value="male"
    checked={isChecked}
  />
  <input
    type="radio"
    id="gender"
    name="gander"
    value="female"
    checked={isChecked}
  />
</div>
<div
  class="input-interface-wrapper std-flex-justify-start std-flex-align-center"
>
  <p class="gender-option-label">gender:</p>
  <div class="gender-option">
    <span class="std-bkg option-selected" />
    <div class="svg-wrapper">
      <svg viewBox="0 0 356 9">
        <path
          d="M3 5.7072C50.1565 5.7072 97.3247 5.92723 144.48 5.64704C193.917 5.3533 243.309 3.75524 292.749 3.51136C312.837 3.41227 332.909 3 353 3"
          stroke="#5B7FFF"
          stroke-width="5"
          stroke-linecap="round"
        />
      </svg>
    </div>
  </div>
</div>

<style>
  .input-wrapper {
    width: 100%;
  }

  .input-wrapper input {
    display: none;
  }
  .input-interface-wrapper {
    width: 100%;
  }

  /* --------- gender option -------- */
  .gender-option-label {
    width: 30%;
  }
  .gender-option {
    width: 30%;
    position: relative;
  }
  .svg-wrapper {
    width: 100%;
  }
  .svg-wrapper svg {
    width: 100%;
  }
</style>
