<script lang="ts">
    export let data;
    $: text = `${data}%`;
</script>

<div class="tip-option">
    <p>{text}</p>
</div>

<style>
    .tip-option {
        border-radius: 5px;
        background-color: rgb(0, 62, 66);
        padding: 8px;
        cursor: pointer;
    }
    .tip-option > p {
        color: white;
        font-weight: 700;
        font-size: 22px;
        text-align: center;
    }
</style>
