<script lang="ts">
    import { createEventDispatcher } from "svelte";
    export let isButtonDisabled;
    export let data;
    const dispatcher = createEventDispatcher();
    $: tipRate = data.tipRate;
    $: bill = data.bill;
    $: numberOfPeople = data.numberOfPeople;
    $: tipAmountPerPerson = (bill * (tipRate / 100)) / numberOfPeople;
    $: isTipAmountPerPersonNaN =
        Number.isNaN(tipAmountPerPerson) || tipAmountPerPerson === 0;
    $: stringifiedTipAmountPerPerson = tipAmountPerPerson.toLocaleString(
        undefined,
        {
            minimumFractionDigits: 2
        }
    );
    $: totalPerPerson = (bill * (1 + tipRate / 100)) / numberOfPeople;
    $: isTotalPerPersonNaN =
        Number.isNaN(totalPerPerson) || totalPerPerson === 0;
    $: stringifiedTotalPerPerson = totalPerPerson.toLocaleString(undefined, {
        minimumFractionDigits: 2
    });
    const resetClickHandler: () => void = () => {
        dispatcher("reset");
        data = {
            tipRate: 0,
            numberOfPeople: 0,
            bill: 0
        };
    };
</script>

<div id="output">
    <div id="tip-amount">
        <div id="tip-amount-text">
            <p>Tip Amount</p>
            <p>/ person</p>
        </div>
        <div id="tip-amount-figure">
            {#if isTipAmountPerPersonNaN}
                <p>$0.00</p>
            {:else}
                <p>${stringifiedTipAmountPerPerson}</p>
            {/if}
        </div>
    </div>
    <div id="total">
        <div id="total-text">
            <p>Total</p>
            <p>/ person</p>
        </div>
        <div id="total-figure">
            {#if isTotalPerPersonNaN}
                <p>$0.00</p>
            {:else}
                <p>${stringifiedTotalPerPerson}</p>
            {/if}
        </div>
    </div>
    <button id="reset" disabled={isButtonDisabled} on:click={resetClickHandler}
        >RESET</button
    >
</div>

<style>
    #output {
        width: 47.5%;
        border-radius: 10px;
        background-color: rgb(0, 62, 66);
        padding: 40px;
        display: flex;
        flex-direction: column;
    }
    #tip-amount {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 30px;
    }
    #tip-amount-text > p:first-child {
        color: rgb(208, 255, 255);
        font-weight: 700;
    }
    #tip-amount-text > p:last-child {
        color: rgb(103, 161, 165);
        font-size: 14px;
    }
    #tip-amount-figure > p {
        color: rgb(31, 186, 161);
        font-weight: 700;
        font-size: 36px;
    }
    #total {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    #total-text > p:first-child {
        color: rgb(208, 255, 255);
        font-weight: 700;
    }
    #total-text > p:last-child {
        color: rgb(103, 161, 165);
        font-size: 14px;
    }
    #total-figure > p {
        color: rgb(31, 186, 161);
        font-weight: 700;
        font-size: 36px;
    }
    #reset {
        margin-top: auto;
        box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 0.1);
        border: none;
        border-radius: 5px;
        padding: 10px;
        font-size: 18px;
        font-weight: 700;
        transition: color 0.3s, background-color 0.3s;
        cursor: pointer;
    }
    #reset:disabled {
        color: rgb(3, 81, 86);
        background-color: rgb(15, 93, 98);
        cursor: auto;
    }
    #reset:enabled {
        background-color: rgb(38, 131, 119);
        color: white;
    }
    #reset:hover {
        background-color: rgb(148, 229, 219);
        color: rgb(0, 42, 39);
    }
    @media all and (max-width: 1440px) {
        #output {
            width: 100%;
        }
        #total {
            margin-bottom: 30px;
        }
    }
</style>
