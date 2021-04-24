<script>
    export let controlType;
    export let id;
    export let label;
    export let value;
    export let rows = 0;
    export let valid = true;
    export let validationMessage = '';

    let touched = false;
</script>

<style>
    input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  border: none;
  border-bottom: 2px solid #ccc;
  border-radius: 3px 3px 0 0;
  background: white;
  padding: 0.15rem 0.25rem;
  transition: border-color 0.1s ease-out;
}

input:focus,
textarea:focus {
  border-color: antiquewhite;
  outline: none;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  width: 100%;
}

.form-control {
  padding: 0.5rem 0;
  width: 100%;
  margin: 0.25rem 0;
}

.invalid {
  border: 1px solid red;
  background: rgb(248, 188, 188);
}

.error-message {
  color: red;
  margin: 0.25rem 0;
}
</style>

<div class="form-control">
    <label for="{id}">{label}</label>
    {#if controlType === "textarea"}
      <textarea class:invalid={!valid && touched} id="{id}" rows="{rows}" bind:value on:blur={() => touched = true}/>
    {:else}
      <input class:invalid={!valid && touched} type="{controlType}" id="{id}" value={value} on:input on:blur={() => touched = true}>
    {/if}
    {#if validationMessage && !valid && touched}
      <p class="error-message">{validationMessage}</p>
    {/if}
</div>