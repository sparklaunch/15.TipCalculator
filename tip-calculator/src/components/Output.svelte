<div id="output">
    <div id="tip-amount">
        <div id="tip-amount-text">
            <p>Tip Amount</p>
            <p>/ person</p>
        </div>
        <div id="tip-amount-figure">
            <p>$0.00</p>
        </div>
    </div>
    <div id="total">
        <div id="total-text">
            <p>Total</p>
            <p>/ person</p>
        </div>
        <div id="total-figure">
            <p>$0.00</p>
        </div>
    </div>
    <button id="reset" disabled={true}>RESET</button>
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
    }
    #reset:disabled {
        border: none;
        border-radius: 5px;
        padding: 10px;
        font-size: 18px;
        font-weight: 700;
        color: rgb(3, 81, 86);
        background-color: rgb(15, 93, 98);
    }
</style>
