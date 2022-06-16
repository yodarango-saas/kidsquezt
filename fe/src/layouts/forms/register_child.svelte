<script lang="ts">
  // excpor let current title
  const currentTitle: number = 0;

  // components
  import RadioInput from "../../chunks/inputs/radio_input.svelte";
  import NumberInput from "../../chunks/inputs/number_input.svelte";
  import TextInput from "../../chunks/inputs/text_input.svelte";
  import Primary from "../../chunks/buttons/primary.svelte";
  import Back from "../..//chunks/buttons/back.svelte";
  import Parragraph from "../../chunks/typography/parragraph.svelte";

  // states
  let currentSection: number = 0;
  let currenstSectionClass: string = "";

  // --------- serve the next portion of the form
  const handleNextFormSection = () => {
    currentSection += 1;
    currenstSectionClass = "swapfwd";
  };

  // --------- serve the previos portion of the form only if teh currentSeciton is greater than 0
  const handlePrevFormSection = () => {
    currentSection -= 1;
    currenstSectionClass = "swapbkwd";
  };
</script>

<div class="form-wrapper">
  <!------- from  ---------->
  <form class="registration-form std-flex-justify-start">
    <!----- first section  -->
    {#if currentSection === 0}
      <div class="form-section-wrapper initial {currenstSectionClass}">
        <TextInput placeholder="first name" />
        <TextInput placeholder="last name" />
        <NumberInput />
        <RadioInput
          value={{ first: "male", second: "femle" }}
          valueLabel={{ first: "m", second: "f" }}
          label="gender"
        />
      </div>

      <!----- second section  -->
    {:else if currentSection === 1}
      <div class="form-section-wrapper {currenstSectionClass}">
        <TextInput placeholder="first name" />
        <TextInput placeholder="last name" />
        <Parragraph
          text="can someone else pick up your child?"
          font="f-secondary"
          color="c-primary"
          align="left"
        />
        <RadioInput
          value={{ first: "yes", second: "no" }}
          valueLabel={{ first: "y", second: "n" }}
        />
      </div>

      <!------- third section  -------->
    {:else}
      <!-- else content here -->
    {/if}
  </form>

  <!------- buttons ---------->
  <div class="button-wrapper_fwd">
    <Primary on:action={handleNextFormSection} />
  </div>

  {#if currentSection > 0}
    <div class="button-wrapper_bkwd">
      <Back on:action={handlePrevFormSection} />
    </div>
  {/if}
</div>

<style>
  /* --------- wrapper -----------  */
  .form-wrapper {
    width: 100%;
    margin: auto;
    position: relative;
  }

  /* ------- form -------- */

  .registration-form {
    width: 100%;
    max-width: 50rem;
    margin: auto;
  }

  /* --------- sections --------- */
  .form-section-wrapper {
    opacity: 0;
    width: 80%;
    margin: auto;
  }

  .initial {
    opacity: 1;
  }

  .form-section-wrapper.swapfwd {
    opacity: 1;
    animation: swapFwd 500ms ease-in;
  }

  .form-section-wrapper.swapbkwd {
    opacity: 1;
    animation: swapBkwd 500ms ease-in;
  }

  @keyframes swapFwd {
    0% {
      opacity: 0;
      transform: translateX(100%);
    }

    99% {
      transform: translateX(0);
    }

    100% {
      opacity: 1;
    }
  }

  @keyframes swapBkwd {
    0% {
      opacity: 0;
      transform: translateX(-100%);
    }

    99% {
      transform: translateX(0);
    }

    100% {
      opacity: 1;
    }
  }

  /* --------- button --------------  */
  .button-wrapper_fwd {
    position: absolute;
    right: 2rem;
    bottom: -8rem;
  }

  .button-wrapper_bkwd {
    position: absolute;
    left: 2rem;
    bottom: -8.2rem;
  }
</style>
