<script lang="ts">
    import { onMount } from 'svelte';

    type Repo = {
        name: string;
        owner: {
            login: string;
        };
        html_url: string;
        description: string;
        stargazers_count: number;
    };

    let selectedRepos: Repo[] = [];

    async function fetchStarredRepos() {
        const response = await fetch('https://api.github.com/users/larspatkowa/starred');
        const data: Repo[] = await response.json();
        selectedRepos = getRandomRepos(data, 3);
    }

    function getRandomRepos(repos: Repo[], count: number): Repo[] {
        const shuffled = repos.sort(() => 0.5 - Math.random());
        return shuffled.slice(0, count);
    }

    onMount(() => {
        fetchStarredRepos();
        const flyIns = document.querySelectorAll('.fly-in');
        flyIns.forEach((element, index) => {
            (element as HTMLElement).style.animationDelay = `${0.1 * (index + 1)}s`;
        });
    });
</script>

<style>
    .fly-in {
        opacity: 0;
        transform: translateY(25%);
        animation: fly-in 0.4s forwards ease-in-out;
    }

    @keyframes fly-in {
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
</style>

<!-- Main -->
<div class="hidden lg:flex flex-col -space-y-6 my-auto fly-in lg:pl-[2%]">
    <h1 class="font-sans select-none -ml-1.5 text-cream text-[128px] xl:text-[178px] font-semibold leading-none">Patkow<span class="tracking-tighter">a</span></h1>
    <div class="select-none">
        <div class="h-[3px] bg-cream"></div>
        <div class="h-[6px] bg-cream mt-2"></div>
        <div class="h-[12px] bg-cream mt-2"></div>
        <div class="h-[24px] bg-cream mt-2"></div>
    </div>
</div>
<div class="relative select-none text-cream my-auto lg:max-w-[45vw] mx-auto flex-1 top-6 lg:top-12 fly-in lg:pr-[6%]">
    <div class="mb-12 fly-in">
        <h2 class="text-[32px] xl:text-[50px] font-semibold leading-none mb-4">about</h2>
            <div class="mt-6 space-y-4">
                    <div class="bg-navyHover p-4 rounded-2xl">
                        <p class="my-0.5 text-xl text-creamHover">not a whole lot to see yet, so, in the meantime, check out some of my stars on github!</p>
                    </div>
            </div>
    </div>

    <div class="fly-in">
        <button type="button" class="flex justify-between w-full font-semibold leading-none mb-4 hover:text-creamHover transition-colors duration-250 cursor-pointer"
            onclick={() => window.location.href = 'https://github.com/larspatkowa?tab=stars'} aria-label="Go to starred repositories">
            <span class="text-[32px] xl:text-[50px]">stars</span>
            <i class="fa-solid fa-up-right-from-square text-[20px] lg:text-[28px] pt-[0.25rem] pr-1"></i>
        </button>
        {#if selectedRepos.length > 0}
            <div class="mt-6 space-y-4">
                {#each selectedRepos as repo}
                    <!-- svelte-ignore a11y_click_events_have_key_events -->
                    <!-- svelte-ignore a11y_no_static_element_interactions -->
                    <div class="bg-navyHover p-4 rounded-2xl cursor-pointer" onclick={()=>window.location.href=repo.html_url}>
                        <div class="flex flex-row justify-between">
                            <a href={repo.html_url} target="_blank" rel="noopener noreferrer" class="text-2xl font-medium text-cream hover:text-creamHover transition-colors duration-250">
                                <span class="font-normal text-creamHover">{repo.owner.login}</span> <span class="text-creamHover font-normal text-xl">/</span> {repo.name}
                            </a>
                            <div class="flex flex-row space-x-2">
                                <i class="fa-solid fa-star text-creamHover mt-1"></i>
                                <span class="inline-block text-creamHover font-semibold text-xl">{repo.stargazers_count}</span>
                            </div>
                        </div>
                        <p class="mt-2 mb-1 text-xl text-creamHover">{repo.description}</p>
                    </div>
                {/each}
            </div>
        {/if}
    </div>
</div>