<script>
  // your script goes here

  import NumberInput from "../../chunks/inputs/number_input.svelte";
  import TextInput from "../../chunks/inputs/text_input.svelte";
</script>

<div>
  <form class="registration-form std-flex-justify-start">
    <TextInput placeholder="first name" />
    <TextInput placeholder="last name" />
    <NumberInput />
  </form>
</div>

<style>
  .registration-form {
    width: 80%;
    max-width: 50rem;
    margin: auto;
  }
</style>
