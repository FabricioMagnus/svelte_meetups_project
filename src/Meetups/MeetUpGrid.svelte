<script>
  import Button from "../UI/Button.svelte";
  import MeetupFilter from "./MeetupFilter.svelte";
  import MeetupItem from "./MeetupItem.svelte";
  import { createEventDispatcher } from "svelte";
  import { scale } from "svelte/transition";
  import { flip } from "svelte/animate";
  export let meetups;

  let FavsOnly = false;

  const dispatch = createEventDispatcher();

  $: filteredMeetups = FavsOnly ? meetups.filter((m) => m.isFavorite) : meetups;

  function setFilter(event) {
    FavsOnly = event.detail === 1;
  }
</script>

<section id="meetup-controls">
  <MeetupFilter on:select={setFilter} />

  <Button on:click={() => dispatch("add")}>New Meetup</Button>
</section>
<section id="meetups">
  {#each filteredMeetups as meetup (meetup.id)}
    <div transition:scale animate:flip>
      <MeetupItem
        id={meetup.id}
        title={meetup.title}
        subtitle={meetup.subtitle}
        description={meetup.description}
        imageUrl={meetup.imageUrl}
        email={meetup.contactEmail}
        address={meetup.address}
        isFav={meetup.isFavorite}
        on:showDetails
        on:edit
      />
    </div>
  {/each}
</section>

<style>
  #meetup-controls {
    margin: "1rem";
    display: flex;
    justify-content: space-evenly;
  }
  #meetups {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 1rem;
  }

  @media (min-width: 768px) {
    #meetups {
      grid-template-columns: repeat(2, 1fr);
    }
  }
</style>
