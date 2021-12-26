<script lang="ts">
    import { onMount } from "svelte";
    import TipOption from "./TipOption.svelte";
    export let tipOptions;
    let billString: string = "";
    $: bill = Number(billString);
    let numberOfPeopleString: string = "";
    $: numberOfPeople = Number(numberOfPeopleString);
    let billInput: HTMLInputElement;
    let numberOfPeopleInput: HTMLInputElement;

    // Courtesy of Stackoverflow...
    function setInputFilter(
        textbox: Element,
        inputFilter: (value: string) => boolean
    ): void {
        [
            "input",
            "keydown",
            "keyup",
            "mousedown",
            "mouseup",
            "select",
            "contextmenu",
            "drop"
        ].forEach(function (event) {
            textbox.addEventListener(
                event,
                function (
                    this: (HTMLInputElement | HTMLTextAreaElement) & {
                        oldValue: string;
                        oldSelectionStart: number | null;
                        oldSelectionEnd: number | null;
                    }
                ) {
                    if (inputFilter(this.value)) {
                        this.oldValue = this.value;
                        this.oldSelectionStart = this.selectionStart;
                        this.oldSelectionEnd = this.selectionEnd;
                    } else if (
                        Object.prototype.hasOwnProperty.call(this, "oldValue")
                    ) {
                        this.value = this.oldValue;
                        if (
                            this.oldSelectionStart !== null &&
                            this.oldSelectionEnd !== null
                        ) {
                            this.setSelectionRange(
                                this.oldSelectionStart,
                                this.oldSelectionEnd
                            );
                        }
                    } else {
                        this.value = "";
                    }
                }
            );
        });
    }
    onMount(() => {
        [billInput, numberOfPeopleInput].forEach((input) => {
            setInputFilter(input, (value) => {
                return /^\d*\.?\d*$/.test(value);
            });
        });
    });
</script>

<div id="calculator">
    <div id="bill">
        <h2>Bill</h2>
        <div id="bill-input">
            <p>$</p>
            <input
                type="text"
                placeholder="0"
                bind:this={billInput}
                bind:value={billString}
            />
        </div>
    </div>
    <div id="tip-selection">
        <h2>Select Tip %</h2>
        <div id="tip-options">
            {#each tipOptions as option}
                <TipOption data={option} />
            {/each}
            <div id="custom-option">
                <p>Custom</p>
            </div>
        </div>
    </div>
    <div id="number-of-people">
        <h2>Number of People</h2>
        <div id="number-of-people-input">
            <img src="/assets/icon-person.svg" alt="Person" />
            <input
                type="text"
                placeholder="0"
                bind:this={numberOfPeopleInput}
                bind:value={numberOfPeopleString}
            />
        </div>
    </div>
</div>

<style>
    #calculator {
        width: 50%;
    }
    #bill {
        display: flex;
        flex-direction: column;
        align-items: stretch;
        margin-bottom: 30px;
    }
    #bill > h2 {
        font-size: 16px;
        color: rgb(86, 103, 102);
        margin-bottom: 3px;
    }
    #bill-input {
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-radius: 10px;
        background-color: rgb(241, 247, 250);
        padding: 10px 20px;
    }
    #bill-input > p {
        font-size: 20px;
        color: rgb(154, 177, 175);
    }
    #bill-input > input {
        border: none;
        background-color: transparent;
        font-size: 20px;
        color: rgb(154, 177, 175);
        text-align: right;
        outline: none;
    }
    #tip-selection {
        display: flex;
        flex-direction: column;
        align-items: stretch;
        margin-bottom: 30px;
    }
    #tip-selection > h2 {
        font-size: 16px;
        color: rgb(86, 103, 102);
        margin-bottom: 10px;
    }
    #tip-options {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        column-gap: 10px;
        row-gap: 10px;
    }
    #custom-option {
        border-radius: 5px;
        background-color: rgb(241, 247, 250);
        padding: 8px;
        cursor: pointer;
    }
    #custom-option > p {
        font-size: 22px;
        font-weight: 700;
        text-align: center;
        color: rgb(66, 97, 93);
    }
    #number-of-people > h2 {
        font-size: 16px;
        color: rgb(86, 103, 102);
        margin-bottom: 3px;
    }
    #number-of-people-input {
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-radius: 10px;
        background-color: rgb(241, 247, 250);
        padding: 10px 20px;
    }
    #number-of-people-input > input {
        border: none;
        background-color: transparent;
        font-size: 20px;
        color: rgb(154, 177, 175);
        text-align: right;
        outline: none;
    }
</style>
