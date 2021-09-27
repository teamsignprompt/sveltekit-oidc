<script lang="ts">
    import { page } from '$app/stores';
    import { isAuthenticated, isLoading, authError, accessToken, LoginButton, LogoutButton } from '$lib';

    import {  getContext } from 'svelte';
    import {
        OIDC_CONTEXT_CLIENT_PROMISE,
        OIDC_CONTEXT_POST_LOGOUT_REDIRECT_URI,
        logout,
    } from '$lib/_keycloak/'/Keycloak.svelte';
    
    import type { OidcContextClientPromise } from '$lib/types';

    const oidcPromise: OidcContextClientPromise = getContext(OIDC_CONTEXT_CLIENT_PROMISE);
    const post_logout_redirect_uri: string = getContext(OIDC_CONTEXT_POST_LOGOUT_REDIRECT_URI);

    let clazz: string = "btn btn-primary";
    export { clazz as class};


</script>

<nav class="w-100 bg-gray-500 flex flex-col justify-center items-center h-12">
    <ul class="list-none flex flex-row w-full h-full justify-center items-center">
        <li class:nav-active={ $page.path === '/' } class="nav-link md:h-full"><a class="text-center font-semibold text-gray-100" sveltekit:prefetch href="/">Home</a></li>
        <li class:nav-active={ $page.path === '/todos' } class="nav-link md:h-full"><a class="text-center font-semibold text-gray-100" sveltekit:prefetch href="/todos">Todos</a></li>
        {#if $isAuthenticated}
            <li>
                <button class={clazz} on:click|preventDefault='{() => logout(oidcPromise, post_logout_redirect_uri) }'></button>
            </li>
        {:else}
            <li><LoginButton class="btn btn-primary">Login</LoginButton></li>
        {/if}
    </ul>
</nav>