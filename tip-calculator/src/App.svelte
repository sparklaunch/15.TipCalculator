<script lang="ts">
    import Card from "./components/Card.svelte";
    const tipOptions: Number[] = [5, 10, 15, 25, 50];
</script>

<div id="app">
    <div id="container">
        <div id="title">
            <h1>SPLI</h1>
            <h1>TTER</h1>
        </div>
        <Card {tipOptions} />
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
    #container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    @media all and (max-width: 1440px) {
        #app {
            height: auto;
            display: block;
            padding-top: 50px;
        }
    }
</style>
