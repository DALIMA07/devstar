<script>
    import HomeLoanCalculator from './HomeLoanCalculator.svelte';
    import InterestCalculator from './InterestCalculator.svelte';
</script>

<div class="card gap-16 items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 overflow-hidden rounded-lg">
    <aside class="calculator-wrapper">
        <InterestCalculator />
    </aside>
    <aside class="calculator-wrapper">
        <HomeLoanCalculator />
    </aside>
</div>

<style>
    .card {
        display: flex;
        flex-direction: column;
        gap: 16px;
        align-items: center;
        margin: auto;
        max-width: 1200px;
        padding: 16px;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        background-color: #f9f9f9;
    }

    @media (min-width: 1024px) {
        .card {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 32px;
            overflow: hidden;
            border-radius: 8px;
        }
    }

    .calculator-wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
    }

    aside {
        width: 100%;
    }
</style>