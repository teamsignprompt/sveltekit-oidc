<script lang="ts">
    import { page } from '$app/stores';
    import { isAuthenticated, isLoading, authError, accessToken, LoginButton, LogoutButton } from '$lib';
    import Header from '../components/shared/Header/index.svelte';
</script>
<Header></Header>
<nav class="w-100 bg-gray-500 flex flex-col justify-center items-center h-12">
    <ul class="list-none flex flex-row w-full h-full justify-center items-center">
        <li class:nav-active={ $page.path === '/' } class="nav-link md:h-full"><a class="text-center font-semibold text-gray-100" sveltekit:prefetch href="/">Home</a></li>
        <li class:nav-active={ $page.path === '/todos' } class="nav-link md:h-full"><a class="text-center font-semibold text-gray-100" sveltekit:prefetch href="/todos">Todos</a></li>
        {#if $isAuthenticated}
            <li><LogoutButton class="btn btn-primary">Logout</LogoutButton></li>
        {:else}
            <li><LoginButton class="btn btn-primary">Login</LoginButton></li>
        {/if}
    </ul>
</nav>