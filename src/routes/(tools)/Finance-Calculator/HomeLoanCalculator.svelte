<script>
    let amount = 0;
    let interestRate = 0;
    let yearTerm = 0;
    let monthlyIncome = 0;
    let emi = 0;
    let totalPayment = 0;
    let totalInterest = 0;
    let remainingIncome = 0;

    function calculateEMI() {
        let monthlyRate = interestRate / 12 / 100;
        let numberOfMonths = yearTerm * 12;
        emi = (amount * monthlyRate * Math.pow(1 + monthlyRate, numberOfMonths)) / (Math.pow(1 + monthlyRate, numberOfMonths) - 1);
        totalPayment = emi * numberOfMonths;
        totalInterest = totalPayment - amount;
        remainingIncome = monthlyIncome - emi;
    }
</script>

<style>
    .calculator {
        max-width: 500px;
        margin: 2rem auto;
        padding: 2rem;
        border: 1px solid #ccc;
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        background-color: #f9f9f9;
    }
    .calculator h2 {
        text-align: center;
        margin-bottom: 1.5rem;
        font-size: 1.5rem;
        color: #333;
    }
    .calculator label {
        display: block;
        font-weight: bold;
        margin-bottom: 0.5rem;
        color: #555;
    }
    .calculator input {
        display: block;
        width: calc(100% - 1rem);
        margin-bottom: 1rem;
        padding: 0.5rem;
        border: 1px solid #ccc;
        border-radius: 5px;
        box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
    }
    .calculator button {
        display: block;
        width: 100%;
        padding: 0.75rem;
        border: none;
        background-color: #007bff;
        color: white;
        border-radius: 5px;
        font-size: 1rem;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    .calculator button:hover {
        background-color: #0056b3;
    }
    .calculator p {
        margin-top: 1rem;
        font-size: 1.1rem;
        color: #333;
    }
</style>

<div class="calculator">
    <h2>Home Loan Calculator</h2>
    <label>
        Loan Amount:
        <input type="number" bind:value={amount} min="0" step="0.01">
    </label>
    <label>
        Annual Interest Rate (%):
        <input type="number" bind:value={interestRate} min="0" step="0.01">
    </label>
    <label>
        Loan Term (years):
        <input type="number" bind:value={yearTerm} min="0" step="0.01">
    </label>
    <label>
        Monthly Income:
        <input type="number" bind:value={monthlyIncome} min="0" step="0.01">
    </label>
    <button on:click={calculateEMI}>Calculate</button>
    {#if emi}
        <p>Monthly EMI: {emi.toFixed(2)}</p>
        <p>Total Payment: {totalPayment.toFixed(2)}</p>
        <p>Total Interest: {totalInterest.toFixed(2)}</p>
        <p>Remaining Income after EMI: {remainingIncome.toFixed(2)}</p>
    {/if}
</div>