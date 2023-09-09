<svelte:options tag="my-counter" />

<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  export let title = '?';

	let count = 0;
  let ref;
 
  function dispatchClick(e) {

    const event = new CustomEvent("customOnClick", {
      detail: { text: "svelte click: " + count },
      bubbles: true,
      cancelable: true,
      composed: true,
    });
    ref.dispatchEvent(event);
  }

	function inc() {
		count++;
	}

	function dec() {
		count--;
	}
</script>

<style>
	* {
		font-size: 200%;
	}

	span {
		width: 4rem;
		display: inline-block;
		text-align: center;
	}

	button {
		width: 64px;
		height: 64px;
		border: none;
		border-radius: 10px;
		background-color: seagreen;
		color: white;
	}
</style>

<button on:click={dec}>
	-
</button>
<span>{count}</span>
<button on:click={inc}>
	+
</button>
<button on:click={dispatchClick} bind:this={ref}>
	{title}
</button>