<script>
    import { createEventDispatcher } from "svelte";
    import TextInput from "../UI/TextInput.svelte";
    import Button from "../UI/Button.svelte";
    import Modal from "../UI/Modal.svelte";
    import {isEmailValid, isEmpty} from "../helpers/validation.js";

    let title = '';
    let subtitle = '';
    let description = '';
    let email = "";
    let address = '';
    let imgUrl = '';

    $: titleValid = !isEmpty(title);
    $: subtitleValid = !isEmpty(subtitle);
    $: descriptionValid = !isEmpty(description);
    $: emailValid = isEmailValid(email);
    $: addressValid = !isEmpty(address);
    $: imgUrlValid = !isEmpty(imgUrl);
    $: formIsValid = titleValid &&
                    subtitleValid &&
                    descriptionValid &&
                    emailValid &&
                    addressValid &&
                    imgUrlValid;

    const dispatch = createEventDispatcher();

    const submitForm = () => {
        dispatch('save', {
            title,
            subtitle,
            description,
            email,
            address,
            imgUrl
        });
    }

    const cancel = () => {
        dispatch('cancel');
    }

</script>

<style>
    form {
        width: 100%;
    }
</style>

<Modal title="Edit Meetup" on:cancel>
    <form on:submit|preventDefault={submitForm}>
        <TextInput 
            id = "title"
            label = "Title"
            controlType = "text"
            valid={titleValid}
            validationMessage="Please enter a valid title"
            value = {title}
            on:input = {(event) => title = event.target.value}
        />
        <TextInput 
            id = "subtitle"
            label = "Subtitle"
            controlType = "text"
            valid={subtitleValid}
            validationMessage="Please enter a valid subtitle"
            value = {subtitle}
            on:input = {(event) => subtitle = event.target.value}
        />
        <TextInput 
            id = "address"
            label = "Address"
            controlType = "text"
            valid={addressValid}
            validationMessage="Please enter a valid address"
            value = {address}
            on:input = {(event) => address = event.target.value}
        />
        <TextInput 
            id = "imgUrl"
            label = "ImgURL"
            controlType = "text"
            valid={imgUrlValid}
            validationMessage="Please enter a valid imgUrl"
            value = {imgUrl}
            on:input = {(event) => imgUrl = event.target.value}
        />
        <TextInput 
            id = "email"
            label = "E-mail"
            controlType = "email"
            valid={emailValid}
            validationMessage="Please enter a valid Email"
            value = {email}
            on:input = {(event) => email = event.target.value}
        />
        <TextInput 
            id = "description"
            label = "Description"
            controlType = "textarea"
            valid={descriptionValid}
            validationMessage="Please enter a valid description"
            rows = 3
            bind:value={description}
        />
    </form>
    <div slot="footer">
        <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
        <Button type="button" on:click={submitForm} disabled="{!formIsValid}">Save</Button>
    </div>
</Modal>