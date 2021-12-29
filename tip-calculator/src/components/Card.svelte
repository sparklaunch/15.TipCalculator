<script lang="ts">
    import Calculator from "./Calculator.svelte";
    import Output from "./Output.svelte";
    export let tipOptions;
    let wasResetClicked: boolean = false;
    let data: Data = {
        tipRate: 0,
        bill: 0,
        numberOfPeople: 0
    };
    let isButtonDisabled: boolean = true;
    interface Data {
        tipRate: number;
        bill: number;
        numberOfPeople: number;
    }
    const enableButtonHandler: () => void = () => {
        isButtonDisabled = false;
    };
    const calculateHandler: (any) => void = (event) => {
        data = event.detail;
    };
    const resetHandler: () => void = () => {
        wasResetClicked = true;
        isButtonDisabled = true;
    };
    const didReset: () => void = () => {
        wasResetClicked = false;
    };
</script>

<div id="card">
    <Calculator
        {tipOptions}
        on:enable-button={enableButtonHandler}
        on:ready-to-calculate={calculateHandler}
        reset={wasResetClicked}
        on:did-reset={didReset}
    />
    <Output {isButtonDisabled} {data} on:reset={resetHandler} />
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
