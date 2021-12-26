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
        box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 0.1);
        justify-content: space-between;
    }
</style>
