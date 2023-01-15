<script>
  // @ts-nocheck

  import { createEventDispatcher } from "svelte";
  import Button from "../UI/Button.svelte";
  import TextInput from "../UI/TextInput.svelte";
  import Modal from "../UI/Modal.svelte";
  import { isEmpty, isValidEmail } from "../helpers/validation";

  let title = "";
  let subtitle = "";
  let address = "";
  let email = "";
  let description = "";
  let imageUrl = "";
  let formIsValid = false;

  $: formIsValid =
    !isEmpty(title) &&
    !isEmpty(subtitle) &&
    !isEmpty(address) &&
    isValidEmail(email) &&
    !isEmpty(description) &&
    !isEmpty(imageUrl);

  const dispatch = createEventDispatcher();

  function submitForm() {
    dispatch("save", {
      title: title,
      subtitle: subtitle,
      address: address,
      email: email,
      description: description,
      imageUrl: imageUrl,
    });
  }

  function closeModal() {
    dispatch("close");
  }
</script>

<Modal title={"Edit MeetUp"} on:close>
  <form on:submit|preventDefault={submitForm}>
    <TextInput
      id="title"
      valid={!isEmpty(title)}
      validityMessage={"Please enter a valid title!"}
      label="Title"
      value={title}
      on:input={(event) => (title = event.target.value)}
    />
    <TextInput
      id="subtitle"
      valid={!isEmpty(subtitle)}
      validityMessage={"Please enter a valid subtitle!"}
      label="Subtitle"
      value={subtitle}
      on:input={(event) => (subtitle = event.target.value)}
    />
    <TextInput
      id="address"
      valid={!isEmpty(address)}
      validityMessage={"Please enter a valid address!"}
      label="Address"
      value={address}
      on:input={(event) => (address = event.target.value)}
    />
    <TextInput
      id="imageUrl"
      valid={!isEmpty(imageUrl)}
      validityMessage={"Please enter a valid imageUrl!"}
      label="Image URL"
      value={imageUrl}
      on:input={(event) => (imageUrl = event.target.value)}
    />
    <TextInput
      id="email"
      valid={isValidEmail(email)}
      validityMessage={"Please enter a valid email!"}
      label="E-Mail"
      type="email"
      value={email}
      on:input={(event) => (email = event.target.value)}
    />
    <TextInput
      id="description"
      label="Description"
      valid={!isEmpty(description)}
      validityMessage={"Please enter a valid description!"}
      controlType="textarea"
      bind:value={description}
    />
  </form>
  <div slot="footer">
    <Button type="button" mode="outline" on:click={closeModal}>Close</Button>
    <Button type="button" disabled={!formIsValid} on:click={submitForm}
      >Save</Button
    >
  </div>
</Modal>

<style>
  form {
    width: 100%;
  }
</style>
