<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./MeetUp/MeetupGrid.svelte";
    import TextInput from "./UI/TextInput.svelte";
    import Button from "./UI/Button.svelte";

    let title = '';
    let subtitle = '';
    let description = '';
    let email = "";
    let address = '';
    let imgUrl = '';

    let meetups = [
        {
            id: 1,
            title: 'Go to walk',
            subtitle: 'In fresh spring forest',
            description: 'We will going in forest all day to evenign, and after that will have a dinner',
            imgUrl: 'https://yobte.ru/uploads/posts/2019-11/the-forest-69-foto-26.jpg',
            address: 'Perm forest',
            contactEmail: 'forest@test.com' 
        }, 
        {
            id: 2,
            title: 'Go to swimm',
            subtitle: 'In big and clean swimming pool',
            description: 'We will swim in clear water and take all positive emotions from this with us',
            imgUrl: 'https://avatars.mds.yandex.net/get-zen_doc/1550999/pub_5d57cb7c46f4ff00ad002728_5d57e136a06eaf00ad1c76ff/scale_1200',
            address: 'Perm swimming pool',
            contactEmail: 'swim@test.com' 
        }
    ];

    const addMeetup = () => {
        const newMeetup = {
            id: Math.random().toString(),
            title: title,
            subtitle: subtitle,
            description: description,
            address: address,
            imgUrl: imgUrl,
            contactEmail: email
        };
        meetups = [newMeetup, ...meetups];
    }
</script>

<style>
    form {
        width: 30rem;
        max-width: 50%;
        margin: auto;
    }
</style>

<Header />

<main>
    <form on:submit|preventDefault={addMeetup}>
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
            rows = 5
            value = {description}
            on:input = {(event) => description = event.target.value}
        />
        <Button type="submit" caption="Save"/>
    </form>

    <MeetupGrid {meetups}/>
</main>



