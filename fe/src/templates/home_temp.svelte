<script lang="ts">
  // components
  import RegisterChild from "../layouts/forms/register_child.svelte";
  import Title from "../chunks/typography/title.svelte";
  import Biggest from "../chunks/images/biggest.svelte";
</script>

<!---------- image ------------->
<div class="image-wrapper">
  <Biggest src="/images/logo.png" alt="kidz quest logo" />
</div>

<!---------- title  ------------->
<Title title="child" />

<!---------- from  ------------->
<RegisterChild />

<style>
  /* ----- image wrapper ----- */
  .image-wrapper {
    width: 100%;
    max-width: 65rem;
  }
</style>
