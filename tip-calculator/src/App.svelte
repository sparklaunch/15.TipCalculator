<script lang="ts">
    import Card from "./components/Card.svelte";
</script>

<div id="app">
    <div id="container">
        <div id="title">
            <h1>SPLI</h1>
            <h1>TTER</h1>
        </div>
        <Card />
    </div>
</div>

<style>
    #app {
        display: flex;
        height: 100%;
        justify-content: center;
        align-items: center;
    }
    #title {
        margin-bottom: 80px;
    }
    #title > h1 {
        color: rgb(54, 88, 90);
        letter-spacing: 8px;
        font-size: 24px;
    }
</style>
