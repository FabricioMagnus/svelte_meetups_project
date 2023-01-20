<script>
  // @ts-nocheck

  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import Button from "./UI/Button.svelte";
  import EditMeetUp from "./Meetups/EditMeetUp.svelte";
  import meetups from "./Meetups/meetups-store";
  import MeetUpDetail from "./Meetups/MeetUp-detail.svelte";

  let addMode = false;
  let editMode = false;
  let detailMode = false;
  let pageData = {};
  let editId;

  function addMeetup() {
    addMode = false;
    editMode = false;
    editId = null;
  }

  function closeModal() {
    addMode = false;
    editMode = false;
    editId = null;
  }

  function closeDetail() {
    detailMode = false;
  }

  function showDetails(event) {
    pageData.id = event.detail;
    detailMode = true;
  }

  function editMeetup(event) {
    editMode = true;
    editId = event.detail;
  }
</script>

<Header />

<main>
  {#if !detailMode}
    {#if addMode || editMode}
      <EditMeetUp on:save={addMeetup} on:close={closeModal} id={editId} />
    {/if}
    <MeetupGrid
      meetups={$meetups}
      on:showDetails={showDetails}
      on:edit={editMeetup}
      on:add={() => {
        addMode = !addMode;
      }}
    />
  {:else}
    <MeetUpDetail id={pageData.id} on:fechar={closeDetail} />
  {/if}
</main>

<style>
  main {
    margin-top: 5rem;
  }
  .meetup-controls {
    margin: 1rem;
  }
</style>
