<script lang="ts">
  // excpor let current title
  export let currentTitle: string = "child";

  // components
  import RadioInput from "../../chunks/inputs/radio_input.svelte";
  import NumberInput from "../../chunks/inputs/number_input.svelte";
  import TextInput from "../../chunks/inputs/text_input.svelte";
  import Primary from "../../chunks/buttons/primary.svelte";
  import Back from "../..//chunks/buttons/back.svelte";
  import Parragraph from "../../chunks/typography/parragraph.svelte";
  import ImageInput from "../../chunks/inputs/image_input.svelte";

  // states
  let currentSection: number = 0;
  let currenstSectionClass: string = "";
  let allowOtherPickUpParty: boolean = false;
  let diplaySubmitForm: boolean = false;

  // --------- chnage the title of the current form section
  const handleTitleChange = (chosenOption) => {
    console.log(chosenOption);
    switch (chosenOption) {
      case 0:
        currentTitle = "child";
        break;
      case 1:
        currentTitle = "guardian";
        break;
      case 2:
        currentTitle = "child";
        break;
    }
  };
  // --------- serve the next portion of the form
  const handleNextFormSection = () => {
    handleTitleChange(currentSection + 1);
    currentSection += 1;
    currenstSectionClass = "swapfwd";
  };

  // --------- serve the previos portion of the form only if teh currentSeciton is greater than 0
  const handlePrevFormSection = () => {
    handleTitleChange(currentSection - 1);
    currentSection -= 1;
    currenstSectionClass = "swapbkwd";
  };

  // ------------ handle the pick up child option
  const handlePickupChildOption = (evt) => {
    const chosenOption = evt.detail.option;

    chosenOption === 1
      ? (allowOtherPickUpParty = true)
      : (allowOtherPickUpParty = false);
  };

  // ----------- handle form submission and child registration
  const handleRegistration = (e) => {
    e.preventDefault();
    console.log(e.serializeArray());
  };
</script>

<div class="form-wrapper">
  <!------- from  ---------->
  <form
    class="registration-form std-flex-justify-start"
    on:submit={handleRegistration}
  >
    <!----- first section  -->
    {#if currentSection === 0}
      <div class="form-section-wrapper initial {currenstSectionClass}">
        <TextInput placeholder="first name" />
        <TextInput placeholder="last name" />
        <NumberInput startAt={4} endAt={11} />
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
        <TextInput placeholder="phone number" type="phone" />
        <Parragraph
          text="is someone else allowed to pick up your child?"
          font="f-secondary"
          color="c-primary"
          align="left"
        />
        <RadioInput
          value={{ first: "yes", second: "no" }}
          valueLabel={{ first: "y", second: "n" }}
          on:action={handlePickupChildOption}
        />

        <!-- allow other pick up -->
        {#if allowOtherPickUpParty}
          <Parragraph
            text="who?"
            font="f-secondary"
            color="c-primary"
            align="left"
          />
          <TextInput placeholder="first name" />
          <TextInput placeholder="last name" />
        {/if}
      </div>

      <!------- third section  -------->
    {:else}
      <div class="form-section-wrapper initial {currenstSectionClass}">
        <div class="input-image-wrapper">
          <ImageInput on:uploadDone={() => (diplaySubmitForm = true)} />
        </div>
      </div>
    {/if}

    {#if diplaySubmitForm}
      <Primary text="Done" type="submit" />
    {/if}
  </form>

  <div class="std-spacer-xl" />
  <div class="std-spacer-xl" />

  <!------- buttons ---------->
  {#if currentSection < 2}
    <div class="button-wrapper_fwd">
      <Primary on:action={handleNextFormSection} text="Next" />
    </div>
  {/if}

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
    bottom: 0rem;
  }

  .button-wrapper_bkwd {
    position: absolute;
    left: 2rem;
    bottom: 0rem;
  }
  .input-image-wrapper {
    margin: var(--medium-spacing) auto 0;
  }
</style>
