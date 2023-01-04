<script>
  import MeetUpItem from "./MeetUpItem.svelte";

  export let meetups;
</script>

<section class="meetups">
  {#each meetups as m (m.id)}
    <MeetUpItem
      title={m.title}
      description={m.description}
      subtitle={m.subtitle}
      address={m.address}
      imageUrl={m.imageUrl}
      email={m.contactEmail}
    />
  {/each}
</section>

<style>
  section {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 1rem;
  }

  @media (min-width: 768px) {
    section {
      grid-template-columns: repeat(2, 1fr);
    }
  }
</style>
