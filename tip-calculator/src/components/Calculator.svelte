<div id="calculator">
    <div id="bill">
        <h2>Bill</h2>
        <div id="bill-input">
            <p>$</p>
            <input type="text" value="0" />
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
</style>
