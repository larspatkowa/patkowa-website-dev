<script lang="ts">
    import '../app.css';
    import '@fortawesome/fontawesome-free/css/all.min.css';
    import Navigation from '$lib/components/Navigation.svelte';
    let { children } = $props();
</script>

<Navigation />

<div class="w-[85%] md:w-[70%] lg:w-[96%] mx-auto lg:min-h-[100vh] flex pb-12 lg:flex-row flex-col justify-between lg:space-x-[8%]">
    {@render children()}
</div>
