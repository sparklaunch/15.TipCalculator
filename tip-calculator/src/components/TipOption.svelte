<script lang="ts">
    import { createEventDispatcher } from "svelte";
    export let data;
    export let index;
    export let active;
    $: text = `${data}%`;
    const dispatcher = createEventDispatcher();
    const clickHandler = (event) => {
        dispatcher("option-clicked", {
            index
        });
    };
</script>

<div class="tip-option" on:click={clickHandler} class:active>
    <p>{text}</p>
</div>

<style>
    .tip-option {
        border-radius: 5px;
        background-color: rgb(0, 62, 66);
        padding: 8px;
        cursor: pointer;
        border: 2px solid transparent;
        transition: background-color 0.3s;
    }
    .tip-option:hover {
        background-color: rgb(148, 229, 219);
    }
    .tip-option:hover > p {
        color: rgb(0, 22, 18);
    }
    .tip-option > p {
        color: white;
        font-weight: 700;
        font-size: 22px;
        text-align: center;
        transition: color 0.3s;
    }
    .active {
        background-color: rgb(35, 186, 164);
        color: rgb(0, 59, 63);
    }
</style>
