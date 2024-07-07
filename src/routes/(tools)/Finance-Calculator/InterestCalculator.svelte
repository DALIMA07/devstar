<script>
    let money = 0;
    let rate = 0;
    let time = 0;
    let interest = 0;

    function calculateInterest() {
        interest = (money * rate * time) / 100;
    }
</script>

<style>
    .calculator {
        max-width: 400px;
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
        text-align: center;
        margin-top: 1rem;
        font-size: 1.25rem;
        color: #333;
    }
</style>

<div class="calculator">
    <h2>Interest Calculator</h2>
    <label>
        Money:
        <input type="number" bind:value={money} min="0" step="0.01">
    </label>
    <label>
        Rate of Interest (%):
        <input type="number" bind:value={rate} min="0" step="0.01">
    </label>
    <label>
        Time (years):
        <input type="number" bind:value={time} min="0" step="0.01">
    </label>
    <button on:click={calculateInterest}>Calculate Interest</button>
    {#if interest}
        <p>Interest: {interest.toFixed(2)}</p>
    {/if}
</div>