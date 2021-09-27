<script lang="ts">
    import { KeycloakProtectedRoute, LogoutButton } from '$lib';
    import Header from '../../components/shared/Header/index.svelte';
</script>

<KeycloakProtectedRoute>
    <Header></Header>
    <div class="h-screen-minus-navbar bg-gray-800 text-white flex flex-col justify-center items-center w-full">
        This is a protected page
        <LogoutButton>Logout</LogoutButton>
    </div>
</KeycloakProtectedRoute>