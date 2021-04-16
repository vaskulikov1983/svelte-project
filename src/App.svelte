<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./MeetUp/MeetupGrid.svelte";

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
    
</style>

<Header />

<main>
    <form on:submit|preventDefault={addMeetup}>
        <div class="form-control">
            <label for="title">Title</label>
            <input type="text" id="title" bind:value={title}>
        </div>
        <div class="form-control">
            <label for="subtitle">Subtitle</label>
            <input type="text" id="subtitle" bind:value={subtitle}>
        </div>
        <div class="form-control">
            <label for="imgUrl">imgUrl</label>
            <input type="text" id="imgUrl" bind:value={imgUrl}>
        </div>
        <div class="form-control">
            <label for="address">Address</label>
            <input type="text" id="adress" bind:value={address}>
        </div>
        <div class="form-control">
            <label for="email">E-mail</label>
            <input type="email" id="email" bind:value={email}>
        </div>
        <div class="form-control">
            <label for="description">Description</label>
            <textarea id="description" rows="5" bind:value={description}></textarea>
        </div>
        <button type="submit">Save</button> 
    </form>

    <MeetupGrid {meetups}/>
</main>



