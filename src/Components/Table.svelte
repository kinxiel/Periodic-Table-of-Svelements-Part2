<script>
  import { elements } from '../Data/PeriodicTableJSON.json';
  import Element from './Element.svelte';

  let selection = {
    // Initial State
    value: 'atomic_mass',
    text: 'Atomic Mass',
  };

  let properties = [
    { value: 'atomic_mass', text: `Atomic Mass` },
    { value: 'boil', text: `Boiling Point` },
    { value: 'category', text: `Category` },
    { value: 'density', text: `Density` },
  ];

  $: selectionProperty = selection.value;
</script>

<style>
  .table {
    display: grid;
    grid-template-columns: repeat(18, auto) 1fr;
    gap: 0.1vw;
  }
  .menu {
    grid-column: 13;
    grid-row: 1;
    grid-column-end: 17;
  }
  .menu select {
    font-size: 1.5vw;
    width: 20vw;
  }
</style>

<div>
  <div class="table text-gray-900">
    <div class="menu">
      <select
        bind:value={selection}
        class="border border-blue-500 shadow sm:mt-2 md:mt-4">
        {#each properties as property}
          <option value={property}><span>{property.text}</span></option>
        {/each}
      </select>
    </div>
    {#each elements as element, i}
      <Element
        atomicNumber={element.number}
        bind:selectedProperty={selectionProperty}
        style="grid-column: {element.xpos}; grid-row: {element.ypos}" />
    {:else}{null}{/each}
  </div>
</div>
