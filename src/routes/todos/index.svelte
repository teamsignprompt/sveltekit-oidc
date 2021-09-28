<script lang="ts">
    import { isAuthenticated, isLoading, authError, KeycloakProtectedRoute, accessToken, LogoutButton } from '$lib';
    import Header from '../../components/shared/Header/index.svelte';
    import { createClient } from '@urql/svelte';
    import { initClient, operationStore, query } from '@urql/svelte';
    import cookie from 'cookie'

    let graphQLEndpoint = `${import.meta.env.VITE_GRAPHQL_ENDPOINT}`;
    let header = `Bearer ${accessToken}`;

    console.log(JSON.stringify(`${accessToken}`));

    let todos = [];

   

    /*initClient({
        url: graphQLEndpoint,
        fetchOptions: () => {
            //const token = ;
            return {
            headers: { 
                'content-type': 'application/json',
                authorization: header
                },
            };
        },
    });

    const todos = operationStore(`
        query MyQuery {
            test_test {
                uuid
            }
        }
    `);

    query(todos);*/

</script>



<KeycloakProtectedRoute>
    <Header></Header>
    <div class="h-screen-minus-navbar bg-gray-800 text-white flex flex-col justify-center items-center w-full">
    {#if $isAuthenticated}
Authenticated...what's going on?
{/if}
        <!--{#if $todos.fetching}
            <p>Loading...</p>
        {:else if $todos.error}
            <p>Oh no... {$todos.error.message}</p>
        {:else}
            <ul>
                {#each $todos.data.test_test as todo}
                <li>{todo.uuid}</li>
                {/each}
            </ul>
        {/if}-->
        <LogoutButton>Logout</LogoutButton>
        ${accessToken}
    </div>
</KeycloakProtectedRoute>