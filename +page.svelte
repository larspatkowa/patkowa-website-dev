<script lang="ts">
    import { onMount } from 'svelte';

    onMount(() => {
        const flyIns = document.querySelectorAll('.fly-in');
        flyIns.forEach((element, index) => {
            (element as HTMLElement).style.animationDelay = `${0.1 * (index + 1)}s`;
        });
    });
</script>

<style>
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        min-height: 100vh;
        text-align: center;
        padding: 2rem;
    }

    h1 {
        font-size: 2.5rem;
        margin-bottom: 1rem;
    }

    p {
        font-size: 1.2rem;
        color: #666;
    }

    .fly-in {
        opacity: 0;
        animation: flyIn 0.8s ease-out forwards;
    }

    @keyframes flyIn {
        from {
            opacity: 0;
            transform: translateY(20px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
</style>

<div class="container">
    <h1 class="fly-in">Coming Soon</h1>
    <p class="fly-in">We're working on something exciting. Stay tuned!</p>
</div>