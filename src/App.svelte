<script>
  // @ts-nocheck

  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import Button from "./UI/Button.svelte";
  import EditMeetUp from "./Meetups/EditMeetUp.svelte";
  import meetups from "./Meetups/meetups-store";
  import MeetUpDetail from "./Meetups/MeetUp-detail.svelte";

  let editMode = false;
  let detailMode = false;
  let pageData = {};

  function addMeetup() {
    editMode = false;
  }

  function closeModal() {
    editMode = false;
  }

  function closeDetail() {
    detailMode = false;
  }

  function showDetails(event) {
    pageData.id = event.detail;
    detailMode = true;
  }
</script>

<Header />

<main>
  {#if !detailMode}
    <div class="meetup-controls">
      <Button on:click={() => (editMode = !editMode)}>New Meetup</Button>
    </div>
    {#if editMode}
      <EditMeetUp on:save={addMeetup} on:close={closeModal} />
    {/if}
    <MeetupGrid meetups={$meetups} on:showDetails={showDetails} />
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
