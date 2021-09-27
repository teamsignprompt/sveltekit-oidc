<script lang="ts">
    import { KeycloakProtectedRoute, accessToken, LogoutButton } from '$lib';
    import Header from '../../components/shared/Header/index.svelte';
    import { createClient } from '@urql/svelte';
    import { initClient, operationStore, query } from '@urql/svelte';

    let graphQLEndpoint = `${import.meta.env.VITE_GRAPHQL_ENDPOINT}`;

    console.log(graphQLEndpoint);

    initClient({
        url: '${graphQLEndpoint}',
        fetchOptions: () => {
            //const token = ;
            return {
            headers: { authorization: accessToken ? `Bearer ${accessToken}` : '' },
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

    query(todos);

</script>

<KeycloakProtectedRoute>
    <Header></Header>
    <div class="h-screen-minus-navbar bg-gray-800 text-white flex flex-col justify-center items-center w-full">
        This is a protected page
        {$accessToken}
        <LogoutButton>Logout</LogoutButton>
    </div>
</KeycloakProtectedRoute>