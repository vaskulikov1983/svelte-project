<script>
    import { createEventDispatcher } from "svelte";
    import TextInput from "../UI/TextInput.svelte";
    import Button from "../UI/Button.svelte";
    import Modal from "../UI/Modal.svelte"

    let title = '';
    let subtitle = '';
    let description = '';
    let email = "";
    let address = '';
    let imgUrl = '';

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
            value = {title}
            on:input = {(event) => title = event.target.value}
        />
        <TextInput 
            id = "subtitle"
            label = "Subtitle"
            controlType = "text"
            value = {subtitle}
            on:input = {(event) => subtitle = event.target.value}
        />
        <TextInput 
            id = "address"
            label = "Address"
            controlType = "text"
            value = {address}
            on:input = {(event) => address = event.target.value}
        />
        <TextInput 
            id = "imgUrl"
            label = "ImgURL"
            controlType = "text"
            value = {imgUrl}
            on:input = {(event) => imgUrl = event.target.value}
        />
        <TextInput 
            id = "email"
            label = "E-mail"
            controlType = "email"
            value = {email}
            on:input = {(event) => email = event.target.value}
        />
        <TextInput 
            id = "description"
            label = "Description"
            controlType = "textarea"
            rows = 3
            value = {description}
            on:input = {(event) => description = event.target.value}
        />
    </form>
    <div slot="footer">
        <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
        <Button type="button" on:click={submitForm}>Save</Button>
    </div>
</Modal>