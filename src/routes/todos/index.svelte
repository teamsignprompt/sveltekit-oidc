<script lang="ts">
    import { KeycloakProtectedRoute, accessToken, LogoutButton } from '$lib';
    import Header from '../../components/shared/Header/index.svelte';
    import { createClient } from '@urql/svelte';
    import { initClient } from '@urql/svelte';

    initClient({
        url: '${import.meta.env.GRAPHQL_ENDPOINT}',
        fetchOptions: () => {
            const token = ${accessToken};
            return {
            headers: { authorization: token ? `Bearer ${token}` : '' },
            };
        },
    });
</script>

<KeycloakProtectedRoute>
    <Header></Header>
    <div class="h-screen-minus-navbar bg-gray-800 text-white flex flex-col justify-center items-center w-full">
        This is a protected page
        
        <LogoutButton>Logout</LogoutButton>
    </div>
</KeycloakProtectedRoute>