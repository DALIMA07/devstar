<script>
  import { onMount } from 'svelte';
  let calculators = [
    {
      title: "ROI Calculator",
      description: "Calculate returns on investments to assess profitability.",
      id: "roi",
    },
    {
      title: "Currency Converter",
      description: "Quickly convert currencies using live exchange rates.",
      id: "currency",
    },
    {
      title: "Salary Calculator",
      description: "Estimate your monthly or annual salary after deductions.",
      id: "salary",
    },
    {
      title: "GST Calculator",
      description: "Calculate Goods and Services Tax for your transactions.",
      id: "gst",
    },
    {
      title: "Home Loan Calculator",
      description: "Estimate your home loan EMIs and total payment.",
      id: "homeLoan",
    },
    {
      title: "TVM Calculator",
      description: "Plan your financial future by calculating Time Value of Money.",
      id: "tvm",
    }
  ];
  
  let selectedCalculator = null;
  
  // ROI Calculator variables and function
    let initialInvestment = 0;
  let returnAmount = 0;
  let years = 0;
  let roi = 0;
  let investmentPeriodMonths = 0;
  let gainOrLoss = 0;
  let simpleAnnualROI = 0;
  let compoundAnnualROI = 0;

  function calculateROI() {
    roi = ((returnAmount - initialInvestment) / initialInvestment) / years;
    investmentPeriodMonths = years * 12;
    gainOrLoss = returnAmount - initialInvestment;
    simpleAnnualROI = (gainOrLoss / initialInvestment) * (1 / years) * 100;
    compoundAnnualROI = Math.pow((returnAmount / initialInvestment), (1 / years)) - 1;
  }

  function resetCalculator() {
    initialInvestment = 0;
    returnAmount = 0;
    years = 0;
    roi = 0;
    investmentPeriodMonths = 0;
    gainOrLoss = 0;
    simpleAnnualROI = 0;
    compoundAnnualROI = 0;
  }

  // Currency Converter variables and function (assuming static exchange rate for simplicity)
  let amount = 0;
  let fromCurrency = 'USD';
  let toCurrency = 'INR';
  let convertedAmount = 0;
  let rates = {};

  onMount(async () => {
    const res = await fetch('https://api.exchangerate-api.com/v4/latest/USD');
    const data = await res.json();
    rates = data.rates;
    convert();
  });

  const convert = () => {
    convertedAmount = (amount * rates[toCurrency]) / rates[fromCurrency];
  };

  const reset = () => {
    amount = 0;
    fromCurrency = 'USD';
    toCurrency = 'INR';
    convertedAmount = 0;
  };

  // Salary Calculator variables and function
  let grossSalary = 0, deductions = 0, netSalary = 0;
  function calculateNetSalary() {
    netSalary = grossSalary - deductions;
  }
  // GST Calculator variables and function
  let priceWithoutGST = 0, gstRate = 18, priceWithGST = 0;
  function calculateGST() {
    priceWithGST = priceWithoutGST * (1 + gstRate / 100);
  }
  // Home Loan Calculator variables and function
  let loanAmount = 0, annualInterestRate = 0, loanTenure = 0, emi = 0, totalPayment = 0;
  function calculateHomeLoan() {
    let monthlyInterestRate = annualInterestRate / 12 / 100;
    let numberOfPayments = loanTenure * 12;
    emi = (loanAmount * monthlyInterestRate) / (1 - Math.pow(1 + monthlyInterestRate, -numberOfPayments));
    totalPayment = emi * numberOfPayments;
  }
  // TVM Calculator variables and function
  let presentValue = 0, interestRate = 0, periods = 0, futureValue = 0;
  function calculateFutureValue() {
    futureValue = presentValue * Math.pow(1 + interestRate / 100, periods);
  }
  function selectCalculator(id) {
    selectedCalculator = id;
  }
</script>

<style>
  .card {
    cursor: pointer;
  }
  
  .calculator {
    border-radius: 8px;
    max-width: 430px;
    box-shadow: 0px -15px 0px rgb(24, 14, 14), 0px 10px 0px rgb(24, 14, 14);
  }
  
  .calculator label {
    display: block;
    margin-top: 8px;
    font-weight: bold;
    margin-bottom: 0.5rem;
    color: #555;
  }
  
  .calculator input {
    margin-top: 4px;
    width: calc(100% - 1rem);
    padding: 8px;
    box-sizing: border-box;
    box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  }
  
</style>

<header class="bg-white py-4 shadow-md sticky top-0 z-10">
  <div class="container mx-auto px-4 flex flex-wrap justify-between items-center text-[#374151] p-3">
    <h1 class="text-2xl font-bold">Craftlab</h1>
    <div class="flex space-x-4 font-semibold text-base md:text-1xl">
      <h1 class="text-blue-700">Home</h1>
      <h1>Free Trial</h1>
      <h1>Information</h1>
      <h1>Calculators</h1>
      <h1>Contact Us</h1>
    </div>
  </div>
</header>
<div class="container mx-auto my-5 p-5">
  <section class="bg-gray-50">
    <div class="py-8 px-4 mx-auto max-w-screen-xl text-center lg:px-12">
      <h1 class="mb-4 text-4xl font-extrabold tracking-tight leading-none text-gray-900 md:text-5xl lg:text-6xl">
        Powerful Financial Calculators at Your Fingertips
      </h1>
      <p class="mb-8 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 xl:px-48">
        Optimize your financial decisions with our comprehensive suite of online calculators.
        Explore our user-friendly tools and harness the full potential of your financial planning.
      </p>
      <div class="px-4 mx-auto text-center md:max-w-screen-md lg:max-w-screen-lg lg:px-36">
        <div class="relative w-full p-2 border bg-white border-gray-300 rounded-lg">
          <div class="flex absolute inset-y-0 items-center text-gray-500 left-0 pl-2.5 pointer-events-none">
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
              <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd"></path>
            </svg>
          </div>
          <input class="hover:border-none block w-full disabled:cursor-not-allowed disabled:opacity-50 pl-11 bg-white text-gray-900 sm:text-base rounded-lg focus:outline-none focus:border-gray-300" placeholder="Search" type="search" />
        </div>
      </div>
    </div>
  </section>
  <section class="container mx-auto my-5 p-5">
    <div class="grid grid-cols-1 sm:grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4">
      {#each calculators as calculator}
        <div class="card block bg-white shadow-md hover:shadow-lg rounded-lg overflow-hidden hover:bg-gray-100" on:click={() => selectCalculator(calculator.id)}>
          <div class="card-content p-4">
            <h5 class="text-lg font-semibold tracking-tight text-gray-900 dark:text-white p-1">
              {calculator.title}
            </h5>
            <p class="card-description text-[#6B7280] p-2 text-base">
              {calculator.description}
            </p>
          </div>
        </div>
      {/each}
    </div>
  </section>
{#if selectedCalculator === 'roi'}

<div class="calculator p-6 rounded-lg shadow-lg max-w-md mx-auto mt-10 mb-10">
  <main class="min-h-screen flex flex-col items-center justify-center bg-gray-100 p-6">
    <div class="justify-center bg-white p-8 rounded shadow-md w-full max-w-md">
      <h1 class="text-2xl font-bold mb-6 text-center">
        ROI Calculator
      </h1>

      <div class=" mb-4">
        <label class="block text-gray-700 mr-2" for="initialInvestment">Initial Investment:</label>
        <input type="number" id="initialInvestment" class="p-2 border border-gray-300 rounded" bind:value={initialInvestment}>
      </div>  

      <div class="mb-4">
        <label class="block text-gray-700 mr-2" for="returnAmount">Return Amount:</label>
        <input type="number" id="returnAmount" class="p-2 border border-gray-300 rounded" bind:value={returnAmount}>
      </div>

      <div class="mb-4">
        <label class="block text-gray-700 mr-2" for="years">Years:</label>
        <input type="number" id="years" class="p-2 border border-gray-300 rounded" bind:value={years}>
      </div>

      <div class="text-center mb-4 mb-8 flex items-center">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-7 rounded mr-2" on:click={calculateROI}>Calculate</button>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-9 rounded ml-2" on:click={resetCalculator}>Reset</button>
      </div>  

      {#if roi !== 0}
        <div class="mt-4 text-black">
          <p>Investment Period: {years} Years ({investmentPeriodMonths} Months)</p>
          <p>Gain or Loss: {gainOrLoss}%</p>
          <p>Return on Investment: {roi.toFixed(2)}%</p>
          <p>Simple Annual ROI: {simpleAnnualROI.toFixed(2)}%</p>
          <p>Compound Annual ROI: {compoundAnnualROI.toFixed(2)}%</p>
        </div>
      {/if} 
    </div>  
  </main>
</div> 
{/if}
{#if selectedCalculator === 'currency'}
<div class="calculator p-6 rounded-lg shadow-lg max-w-md mx-auto mt-10 mb-10"> 
  <main class="min-h-screen flex flex-col items-center justify-center bg-gray-100 p-6">
    <div class="bg-white p-8 rounded shadow-md w-full max-w-md ">
      <h1 class="text-2xl font-bold mb-6 text-center">Currency Convertor</h1>
      <div class="mb-4">
        <label class="block text-gray-700 mb-2" for="amount">Amount :</label>
        <input type="number" id="amount" bind:value={amount} class="w-full p-2 border border-gray-300 rounded" />
      </div>
      
      <div class="flex mb-4">
        <div class="flex-1 mr-2 flex items-center">
          <label class="block text-gray-700 mr-2" for="fromCurrency">From:</label>
          <select id="fromCurrency" bind:value={fromCurrency} class="w-full p-2 border border-gray-300 rounded">
            {#each Object.keys(rates) as currency}
              <option value={currency}>{currency}</option>
            {/each}
          </select>
        </div>
        <div class="flex-1 ml-2 flex items-center">
          <label class="block text-gray-700 mr-2" for="toCurrency">To:</label>
          <select id="toCurrency" bind:value={toCurrency} class="w-full p-2 border border-gray-300 rounded">
            {#each Object.keys(rates) as currency}
              <option value={currency}>{currency}</option>
            {/each}
          </select>
        </div>
      </div>
      
      <div class="text-center mb-4 mb-8 flex items-center">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-10 rounded mr-2" on:click={convert}>Convert</button>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-11 rounded ml-2" on:click={reset}>Reset</button>
      </div>
        
      <div class="text-center">
        <p class="text-xl font-semibold ">Converted Amount:</p>
        <p class="text-2xl font-bold">{convertedAmount.toFixed(2)} {toCurrency}</p>
      </div>
      
    </div>
  </main>
</div>
{/if}
{#if selectedCalculator === 'salary'}
  <div class="calculator p-6 rounded-lg shadow-lg max-w-md mx-auto mt-10 mb-10">
    <h2 class="text-2xl font-bold mb-4 text-center   py-2 rounded-lg">Salary Calculator</h2>
    <label class="block mb-2">
      Gross Salary:
      <input type="number" bind:value={grossSalary} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <label class="block mb-2">
      Deductions:
      <input type="number" bind:value={deductions} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <button on:click={calculateNetSalary} class="bg-green-500 text-white py-2 px-4 rounded w-full font-bold">
      Calculate Net Salary
    </button>
      <p class="mt-4 text-lg font-semibold">Net Salary: {netSalary.toFixed(2)}</p>
  </div>
{/if}
{#if selectedCalculator === 'gst'}
  <div class="calculator p-6 rounded-lg shadow-lg max-w-md mx-auto mt-10 mb-10">
    <h2 class="text-2xl font-bold mb-4 text-center py-2 rounded-lg">GST Calculator</h2>
    <label class="block mb-2">
      Price without GST:
      <input type="number" bind:value={priceWithoutGST} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <label class="block mb-2">
      GST Rate (%):
      <input type="number" bind:value={gstRate} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <button on:click={calculateGST} class="bg-yellow-400 text-white py-2 px-4 rounded w-full font-bold">
      Calculate Price with GST
    </button>
      <p class="mt-4 text-lg font-semibold">Price with GST: {priceWithGST.toFixed(2)}</p>
  </div>
{/if}
{#if selectedCalculator === 'homeLoan'}
  <div class="calculator p-6 rounded-lg shadow-lg max-w-md mx-auto mt-10 mb-10">
    <h2 class="text-2xl font-bold mb-4 text-center   py-2 rounded-lg">Home Loan Calculator</h2>
    <label class="block mb-2">
      Loan Amount:
      <input type="number" bind:value={loanAmount} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <label class="block mb-2">
      Annual Interest Rate (%):
      <input type="number" bind:value={annualInterestRate} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <label class="block mb-2">
      Loan Tenure (years):
      <input type="number" bind:value={loanTenure} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <button on:click={calculateHomeLoan} class="bg-purple-500 text-white py-2 px-4 rounded w-full font-bold">
      Calculate EMI
    </button>
      <p class="mt-4 text-lg font-semibold">EMI: {emi.toFixed(2)}</p>
    <p>Total Payment: {totalPayment.toFixed(2)}</p>
  </div>
{/if}
{#if selectedCalculator === 'tvm'}
  <div class="calculator p-6 rounded-lg shadow-lg max-w-md mx-auto mt-10 mb-10">
    <h2 class="text-2xl font-bold mb-4 text-center  py-2 rounded-lg">TVM Calculator</h2>
    <label class="block mb-2">
      Present Value:
      <input type="number" bind:value={presentValue} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <label class="block mb-2">
      Interest Rate (%):
      <input type="number" bind:value={interestRate} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <label class="block mb-2">
      Number of Periods:
      <input type="number" bind:value={periods} class="border border-gray-300 rounded w-full py-2 px-3 mt-1" />
    </label>
    <button on:click={calculateFutureValue} class="bg-indigo-500 text-white py-2 px-4 rounded w-full font-bold">
      Calculate Future Value
    </button>
      <p class="mt-4 text-lg font-semibold">Future Value: {futureValue.toFixed(2)}</p>
  </div>
{/if}
  <footer class="bg-gray-100 py-4 text-center mt-10">
    <p class="text-gray-600">&copy; All rights reserved.</p>
  </footer>
</div>
