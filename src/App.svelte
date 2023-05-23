<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import TextInput from "./UI/TextInput.svelte";
  import Button from "./UI/Button.svelte";

    let title = ""
    let subtitle = ""
    let address = ""
    let email = ""
    let description = ""
    let imageUrl = ""

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'This is the meeting description.',
            imageUrl: 'https://images.unsplash.com/photo-1684528905602-236109cf45c5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=387&q=80',
            address: 'HCM City',
            contactEmail: 'code@test.com'
        },
        {
            id: 'm2',
            title: 'Another Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'This is the meeting description.',
            imageUrl: 'https://images.unsplash.com/photo-1684528905602-236109cf45c5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=387&q=80',
            address: 'HCM City',
            contactEmail: 'code@test.com'
        }
    ]

    function addMeetup() {
        const newMeetup = {
            id: Math.random().toString(),
            title, subtitle, description, imageUrl, address,
            contactEmail: email
        }     
        
        meetups = [newMeetup, ...meetups]
    }
</script>

<style>
    main {
        margin-top: 5rem;
    }

    form {
        width: 30rem;
        max-width: 90%;
        margin: auto;
    }
</style>


<Header />

<main>
    <form on:submit|preventDefault="{addMeetup}">
        <TextInput 
            id="title" 
            label="Title" 
            value={title} 
            type="text"
            on:input={event => (title = event.target.value)}  
        />
        <TextInput 
            id="subtitle" 
            label="Subtitle" 
            value={subtitle} 
            type="text"
            on:input={event => (subtitle = event.target.value)}  
        />
        <TextInput 
            id="address" 
            label="Address" 
            value={address} 
            type="text"
            on:input={event => (address = event.target.value)}  
        />
        <TextInput 
            id="imageUrl" 
            label="Image URL" 
            value={imageUrl} 
            type="text"
            on:input={event => (imageUrl = event.target.value)}  
        />
        <TextInput 
            id="email" 
            label="Email" 
            value={email} 
            type="email"
            on:input={event => (email = event.target.value)}  
        />
        <TextInput 
            id="description" 
            label="Description" 
            value={description} 
            controlType="textarea"
            on:input={event => (description = event.target.value)}  
        />
        
        <Button type="submit" caption="Save" />
    </form>
    <MeetupGrid {meetups} />
</main>