<script lang="ts">
    const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "."];
    const operations = ["/", "x", "-", "+", "="];

    let selectedOperation = "";
    let display = "";
    let firstNumber = "";
    let secondNumber = "";
    let isDisplayingResults = false;

    const handleOperationClick = (operation: string) => {
        if (!firstNumber && display) {
            firstNumber = display;
            selectedOperation = operation;
        } else if (firstNumber) {
            if (!secondNumber && operation === "=") {
                secondNumber = display;
                const firstNum = parseInt(firstNumber);
                const secondNum = parseInt(secondNumber);
                let results = "";

                switch (selectedOperation) {
                    case "/":
                        results = (firstNum / secondNum).toFixed(2);
                        break;
                    case "x":
                        results = (firstNum * secondNum).toFixed(2);
                        break;
                    case "+":
                        results = (firstNum + secondNum).toFixed(2);
                        break;
                    case "-":
                        results = (firstNum - secondNum).toFixed(2);
                        break;
                }
                display = results;
                isDisplayingResults = true;
                selectedOperation = "";
            }
            else {
                
            }
        }
    };

    const handleNumberClick = (number: string) => {
        const zeroComma = "0.";
        if (selectedOperation && firstNumber === display) {
            display = "";
        }
        if (display === "") {
            display = number === "." ? zeroComma : number;
        } else if (display === "0") {
            display = number === "." ? zeroComma : number;
        } else if (display.includes(".") && number === ".") return;
        else {
            display = `${display}${number}`;
        }
    };
    const handleClear = () => {
        display = "";
        firstNumber = "";
        secondNumber = "";
        selectedOperation = "";
    };
</script>

<main>
    <div class="calculator">
        <div class="results">
            {display}
        </div>
        <div class="digits">
            <div class="numbers">
                <button class="btn btn-xlg" on:click={() => handleClear()}
                    >C</button
                >
                {#each numbers as number (number)}
                    <button
                        class={`btn ${number === "0" ? "btn-lg" : null}`}
                        on:click={() => handleNumberClick(number)}
                        >{number}</button
                    >
                {/each}
            </div>
            <div class="operations">
                {#each operations as operation (operation)}
                    <button
                        class={`btn btn-${
                            operation === selectedOperation
                                ? "silver"
                                : "orange"
                        }`}
                        on:click={() => handleOperationClick(operation)}
                        >{operation}</button
                    >
                {/each}
            </div>
        </div>
    </div>
</main>

<style>
    main {
        width: 100vw;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .calculator {
        background-color: rgb(28, 28, 28);
        width: 240px;
        padding: 15px;
        border-radius: 7px;
    }
    .digits {
        display: flex;
    }
    .operations {
        display: flex;
        flex-direction: column;
    }
    .numbers {
        display: flex;
        flex-wrap: wrap;
        width: 200px;
    }
    .btn {
        width: 50px;
        height: 50px;
        border-radius: 100px;
        background-color: rgb(114, 113, 113);
        font-size: 20px;
        font-weight: bold;
        color: white;
        margin: 5px;
        border: none;
    }
    .btn-lg {
        width: 110px;
    }
    .btn-orange {
        background-color: orange;
    }
    .btn-silver {
        background-color: silver;
    }
    .btn-xlg {
        width: 170px;
    }
    .results {
        height: 60px;
        color: white;
        font-size: 50px;
        display: flex;
        flex-direction: row-reverse;
        margin-right: 10px;
    }
</style>
