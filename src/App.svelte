<script>
  // @ts-nocheck

  import Header from "./UI/Header.svelte";
  import MeetupGrid from "./Meetups/MeetupGrid.svelte";
  import Button from "./UI/Button.svelte";
  import EditMeetUp from "./Meetups/EditMeetUp.svelte";
  import meetups from "./Meetups/meetups-store";

  let editMode = false;

  function addMeetup(event) {
    const meetUpData = {
      title: event.detail.title,
      subtitle: event.detail.subtitle,
      description: event.detail.description,
      imageUrl: event.detail.imageUrl,
      contactEmail: event.detail.email,
      address: event.detail.address,
    };
    // meetups.push(newMeetup); // DOES NOT WORK!
    meetups.addMeetup(meetUpData);
    editMode = false;
  }

  function toggleFavorite(event) {
    const id = event.detail;
    meetups.toggleFavorite(id);
  }

  function closeModal() {
    editMode = false;
  }
</script>

<Header />

<main>
  <div class="meetup-controls">
    <Button on:click={() => (editMode = !editMode)}>New Meetup</Button>
  </div>
  {#if editMode}
    <EditMeetUp on:save={addMeetup} on:close={closeModal} />
  {/if}
  <MeetupGrid meetups={$meetups} on:togglefavorite={toggleFavorite} />
</main>

<style>
  main {
    margin-top: 5rem;
  }
  .meetup-controls {
    margin: 1rem;
  }
</style>
