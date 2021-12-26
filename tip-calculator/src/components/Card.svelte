<script lang="ts">
    import Calculator from "./Calculator.svelte";
    import Output from "./Output.svelte";
    export let tipOptions;
</script>

<div id="card">
    <Calculator {tipOptions} />
    <Output />
</div>

<style>
    #card {
        border-radius: 20px;
        background-color: white;
        padding: 40px;
        display: flex;
        width: 800px;
    }
</style>
