<script lang="ts">
    import { afterUpdate, onMount } from "svelte";
    import TipOption from "./TipOption.svelte";
    export let tipOptions;
    let billString: string = "";
    $: bill = Number(billString);
    let numberOfPeopleString: string = "";
    $: numberOfPeople = Number(numberOfPeopleString);
    let billInput: HTMLInputElement;
    let numberOfPeopleInput: HTMLInputElement;
    let isBillFocused: boolean = false;
    let isNumberOfPeopleFocused: boolean = false;
    let isCustomOptionEnabled: boolean = false;
    let customOptionField: HTMLInputElement;
    let isBillZero: boolean = false;
    let isNumberOfPeopleZero: boolean = false;

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
    const focusHandler: (any) => void = (event) => {
        if (event.target.id === "input-bill") {
            isBillFocused = true;
        } else if (event.target.id === "input-number-of-people") {
            isNumberOfPeopleFocused = true;
        }
    };
    const blurHandler: (any) => void = (event) => {
        const isZero: RegExp = new RegExp(/^[0\.]*$/);
        if (event.target.id === "input-bill") {
            billString = String(bill);
            isBillFocused = false;
            if (isZero.test(event.target.value)) {
                isBillZero = true;
            } else {
                isBillZero = false;
            }
        } else if (event.target.id === "input-number-of-people") {
            isNumberOfPeopleFocused = false;
            numberOfPeopleString = String(numberOfPeople);
            if (isZero.test(event.target.value)) {
                isNumberOfPeopleZero = true;
            } else {
                isNumberOfPeopleZero = false;
            }
        }
    };
    const customOptionClickHandler: (any) => void = (event) => {
        isCustomOptionEnabled = true;
    };
    const windowClickHandler: (any) => void = (event) => {
        const id: string = event.target.id;
        if (
            id !== "custom-option" &&
            id !== "custom-label" &&
            id !== "custom-input"
        ) {
            isCustomOptionEnabled = false;
        }
    };
    onMount(() => {
        [billInput, numberOfPeopleInput].forEach((input) => {
            setInputFilter(input, (value) => {
                return /^\d*\.?\d*$/.test(value);
            });
        });
    });
    afterUpdate(() => {
        if (customOptionField) {
            setInputFilter(customOptionField, (value) => {
                return /^\d*\.?\d*$/.test(value);
            });
        }
        if (customOptionField && isCustomOptionEnabled) {
            customOptionField.focus();
        }
    });
</script>

<svelte:window on:click={windowClickHandler} />
<div id="calculator">
    <div id="bill">
        <h2>Bill</h2>
        {#if isBillZero}
            <p class="warning-zero">Can't be zero</p>
        {/if}
        <div
            id="bill-input"
            class:focused={isBillFocused}
            class:warning={isBillZero}
        >
            <img src="/assets/icon-dollar.svg" alt="Dollar Sign" />
            <input
                type="text"
                id="input-bill"
                placeholder="0"
                bind:this={billInput}
                bind:value={billString}
                on:focus={focusHandler}
                on:blur={blurHandler}
            />
        </div>
    </div>
    <div id="tip-selection">
        <h2>Select Tip %</h2>
        <div id="tip-options">
            {#each tipOptions as option}
                <TipOption data={option} />
            {/each}
            <div
                id="custom-option"
                class:focused={isCustomOptionEnabled}
                on:click={customOptionClickHandler}
            >
                {#if !isCustomOptionEnabled}
                    <p id="custom-label">Custom</p>
                {:else}
                    <input
                        type="text"
                        id="custom-input"
                        bind:this={customOptionField}
                    />
                {/if}
            </div>
        </div>
    </div>
    <div id="number-of-people">
        <h2>Number of People</h2>
        {#if isNumberOfPeopleZero}
            <p class="warning-zero">Can't be zero</p>
        {/if}
        <div
            id="number-of-people-input"
            class:focused={isNumberOfPeopleFocused}
            class:warning={isNumberOfPeopleZero}
        >
            <img src="/assets/icon-person.svg" alt="Person" />
            <input
                type="text"
                id="input-number-of-people"
                placeholder="0"
                bind:this={numberOfPeopleInput}
                bind:value={numberOfPeopleString}
                on:focus={focusHandler}
                on:blur={blurHandler}
            />
        </div>
    </div>
</div>

<style>
    #calculator {
        width: 47.5%;
    }
    #bill {
        display: flex;
        flex-direction: column;
        align-items: stretch;
        margin-bottom: 30px;
        position: relative;
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
        border: 2px solid transparent;
        transition: border 0.3s;
    }
    #bill-input > input {
        border: none;
        font-weight: 700;
        background-color: transparent;
        font-size: 20px;
        color: rgb(154, 177, 175);
        text-align: right;
        outline: none;
        cursor: pointer;
        transition: color 0.3s;
    }
    #bill-input > input:focus {
        color: rgb(0, 29, 12);
        font-weight: 700;
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
        transition: background-color 0.3s, border 0.3s;
        border: 2px solid transparent;
        outline: none;
    }
    #custom-option:hover {
        background-color: rgb(148, 229, 219);
    }
    #custom-option > p {
        font-size: 22px;
        font-weight: 700;
        text-align: center;
        color: rgb(66, 97, 93);
    }
    #custom-option > input {
        outline: none;
        background-color: transparent;
        width: 100%;
        border: none;
        font-size: 22px;
        font-weight: 700;
        text-align: center;
        color: rgb(0, 26, 18);
    }
    #number-of-people {
        position: relative;
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
        border: 2px solid transparent;
        transition: border 0.3s;
    }
    #number-of-people-input > input {
        border: none;
        background-color: transparent;
        font-size: 20px;
        font-weight: 700;
        color: rgb(154, 177, 175);
        text-align: right;
        outline: none;
        cursor: pointer;
        transition: color 0.3s;
    }
    #number-of-people-input > input:focus {
        color: rgb(0, 42, 51);
    }
    .focused {
        border: 2px solid rgb(81, 162, 152) !important;
    }
    .warning {
        border: 2px solid rgb(198, 114, 99) !important;
    }
    .warning-zero {
        position: absolute;
        top: 0;
        right: 0;
        font-size: 16px;
        font-weight: 700;
        color: rgb(198, 114, 99);
    }
</style>
