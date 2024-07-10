<script>	
	let calculators = [
	  {
		title: "Time Value of Money (TVM) Calculator",
		description: "Plan your financial future by calculating Time Value of Money.",
		id: "tvm",
	  },
	  {
		title: "Currency Converter",
		description: "Quickly convert currencies using live exchange rates.",
		id: "currency",
	  },
	  {
		title: "Compound Interest Calculator",
		description: "Estimate your earnings with compound interest calculations.",
		id: "compoundInterest",
	  },
	  {
		title: "Return On Investment (ROI) Calculator",
		description: "Calculate returns on investments to assess profitability.",
		id: "roi",
	  },
	  {
		title: "Internal Rate of Return (IRR) and Net Present Value (NPV) Calculator",
		description: "Evaluate investment projects using IRR and NPV for financial analysis.",
		id: "irrNpv",
	  },
	  {
		title: "Bond Price and Yield Calculator",
		description: "Calculate bond prices and yields for investment decisions.",
		id: "bondPriceYield",
	  },
	];
	
	
  
  
  </script>
  
  <style>
	.card {
	  cursor: pointer;
	}
	.calculator {
	  border: 1px solid #ccc;
	  padding: 16px;
	  border-radius: 8px;
	  max-width: 400px;
	  margin: auto;
	  margin-top: 20px;
	}
  </style>
  
  <header class="bg-white py-4 shadow-md sticky top-0 z-10 overflow-hidden">
	<div class="container mx-auto px-4 flex flex-wrap justify-between items-center text-[#374151] p-3">
	  <h1 class="text-2xl font-bold">Craftlab</h1>
	  <div class="space-x-4 font-semibold text-base md:text-1xl md:flex hidden">
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
	  <div class="py-8 px-4 mx-auto max-w-screen-xl text-center lg:px-12 xl:px-16">
		<h1 class="mb-4 text-4xl font-extrabold tracking-tight leading-none text-gray-900 md:text-5xl lg:text-6xl xl:text-7xl">
		  Powerful Financial Calculators at Your Fingertips
		</h1>
		<p class="mb-8 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 xl:px-48">
		  Optimize your financial decisions with our comprehensive suite of online calculators.
		  Explore our user-friendly tools and harness the full potential of your financial planning.
		</p>
		<div class="px-4 mx-auto text-center md:max-w-screen-md lg:max-w-screen-lg xl:max-w-screen-xl lg:px-36 xl:px-48">
		  <div class="relative w-full p-2 border bg-white border-gray-300 rounded-lg">
			<div class="flex absolute inset-y-0 items-center text-gray-500 left-0 pl-2.5 pointer-events-none">
			  <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
				<path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd"></path>
			  </svg>
			</div>
			<input class="hover:border-none border-none block w-full disabled:cursor-not-allowed disabled:opacity-50 pl-11 bg-white text-gray-900 sm:text-base rounded-lg focus:outline-none outline-none" placeholder="Search" type="search" />
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
  
  
	<footer class="bg-gray-100 py-4 text-center">
	  <p class="text-gray-600">&copy; All rights reserved.</p>
	</footer>
  </div>
  