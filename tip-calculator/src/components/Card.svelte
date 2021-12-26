<script lang="ts">
    import Calculator from "./Calculator.svelte";
    import Output from "./Output.svelte";
</script>

<div id="card">
    <Calculator />
    <Output />
</div>

<style>
    #card {
        border-radius: 20px;
        background-color: white;
        padding: 30px;
        display: flex;
        width: 800px;
    }
</style>
