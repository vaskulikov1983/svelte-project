<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./MeetUp/MeetupGrid.svelte";
    import TextInput from "./UI/TextInput.svelte";
    import Button from "./UI/Button.svelte";
    import EditMeetup from "./MeetUp/EditMeetup.svelte";

    let editMode;

    let meetups = [
        {
            id: 1,
            title: 'Go to walk',
            subtitle: 'In fresh spring forest',
            description: 'We will going in forest all day to evenign, and after that will have a dinner',
            imgUrl: 'https://yobte.ru/uploads/posts/2019-11/the-forest-69-foto-26.jpg',
            address: 'Perm forest',
            contactEmail: 'forest@test.com',
            isFavorite: false
        }, 
        {
            id: 2,
            title: 'Go to swimm',
            subtitle: 'In big and clean swimming pool',
            description: 'We will swim in clear water and take all positive emotions from this with us',
            imgUrl: 'https://avatars.mds.yandex.net/get-zen_doc/1550999/pub_5d57cb7c46f4ff00ad002728_5d57e136a06eaf00ad1c76ff/scale_1200',
            address: 'Perm swimming pool',
            contactEmail: 'swim@test.com',
            isFavorite: false
        }
    ];

    const addMeetup = (event) => {
        const newMeetup = {
            id: Math.random().toString(),
            title: event.detail.title,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            address: event.detail.address,
            imgUrl: event.detail.imgUrl,
            contactEmail: event.detail.email
        };

        meetups = [newMeetup, ...meetups];

        editMode = null;
    }

    const toggleFavorite = (evt) => {
        const id = evt.detail;
        const updatedMeetup = {...meetups.find(item => item.id === id)};
        updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
        const meetupIndex = meetups.findIndex(item => item.id === id);
        const updatedMeetups = [...meetups];
        updatedMeetups[meetupIndex] = updatedMeetup;
        meetups = updatedMeetups;

    };

    const cancelModal = () => {
        editMode = null;
    }
</script>

<style>
    main {
        padding-top: 20px;
    }
    .meetup-controls {
        margin: 1rem;
    }
</style>

<Header />

<main>
    <div class="meetup-controls">
        <Button on:click={() => editMode = "add"}>New Meetup</Button>
    </div>
    {#if editMode === "add"}
        <EditMeetup on:save={addMeetup} on:cancel={cancelModal}/>
    {/if}
    <MeetupGrid {meetups} on:toggleFavorite={toggleFavorite}/>
</main>



