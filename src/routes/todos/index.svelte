<script lang="ts">
    import { KeycloakProtectedRoute, accessToken, LogoutButton } from '$lib';
    import Header from '../../components/shared/Header/index.svelte';
    import { createClient } from '@urql/svelte';
    import { initClient, operationStore, query } from '@urql/svelte';

    initClient({
        url: '${import.meta.env.GRAPHQL_ENDPOINT}',
        fetchOptions: () => {
            //const token = ;
            return {
            headers: { authorization: token ? `Bearer ${accessToken}` : '' },
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
        
        <LogoutButton>Logout</LogoutButton>
    </div>
</KeycloakProtectedRoute>