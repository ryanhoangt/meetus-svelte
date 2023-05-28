<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import Button from "./UI/Button.svelte";
    import EditMeetup from "./Meetups/EditMeetup.svelte";

    let editMode = null

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'This is the meeting description.',
            imageUrl: 'https://images.unsplash.com/photo-1684528905602-236109cf45c5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=387&q=80',
            address: 'HCM City',
            contactEmail: 'code@test.com',
            isFavorite: false
        },
        {
            id: 'm2',
            title: 'Another Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'This is the meeting description.',
            imageUrl: 'https://images.unsplash.com/photo-1684528905602-236109cf45c5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=387&q=80',
            address: 'HCM City',
            contactEmail: 'code@test.com',
            isFavorite: false
        }
    ]

    function addMeetup(event) {
        const newMeetup = {
            id: Math.random().toString(),
            title: event.detail.title, 
            subtitle: event.detail.subtitle, 
            description: event.detail.description, 
            imageUrl: event.detail.imageUrl, 
            address: event.detail.address,
            contactEmail: event.detail.email
        }     
        
        meetups = [newMeetup, ...meetups]
        editMode = null
    }

    function toggleFavorite(event) {
        const id = event.detail
        const updatedMeetup = {...meetups.find(m => m.id === id)}
        updatedMeetup.isFavorite = !updatedMeetup.isFavorite

        const meetupIndex = meetups.findIndex(m => m.id === id)
        const newMeetups = [...meetups]
        newMeetups[meetupIndex] = updatedMeetup
        meetups = newMeetups
    }

    function cancelEdit() {
        editMode = null
    }
</script>

<Header />
<main>
    <div class="meetup-controls">

    </div>

    <Button on:click="{() => editMode = "add"}">New Meetup</Button>
    {#if editMode === "add"}
        <EditMeetup on:save="{addMeetup}" on:cancel={cancelEdit} />
    {/if}
    <MeetupGrid {meetups} on:togglefavorite="{toggleFavorite}" />

</main>


<style>
    main {
        margin-top: 5rem;
    }

    .meetup-controls {
        margin: 1rem;

    }
</style>

