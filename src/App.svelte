<script>
  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import Button from "./UI/Button.svelte";
  import EditMeetup from "./Meetups/EditMeetup.svelte";
  import meetupsStore from "./Meetups/meetups-store";
  import MeetupDetail from "./Meetups/MeetupDetail.svelte";

  let editMode = null;
  let page = "overview";
  let pageData = {};
  let editingId = null;

  function saveMeetup(event) {
    editMode = null;
    editingId = null;
  }

  function cancelEdit() {
    editMode = null;
    editingId = null;
  }

  function showDetails(event) {
    page = "details";
    pageData.id = event.detail;
  }

  function closeDetails() {
    page = "overview";
    pageData = {};
  }

  function startEdit(event) {
    editMode = "edit";
    editingId = event.detail;
  }
</script>

<Header />
<main>
  {#if page === "overview"}
    {#if editMode === "edit"}
      <EditMeetup on:save={saveMeetup} on:cancel={cancelEdit} id={editingId} />
    {/if}
    <MeetupGrid
      meetups={$meetupsStore}
      on:showdetails={showDetails}
      on:edit={startEdit}
      on:add={() => (editMode = "edit")}
    />
  {:else}
    <MeetupDetail id={pageData.id} on:close={closeDetails} />
  {/if}
</main>

<style>
  main {
    margin-top: 5rem;
  }
</style>
