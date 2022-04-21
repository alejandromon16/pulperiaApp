<script>
    import SideMenu from '$lib/components/sideMenu.svelte';
    import Head from '$lib/components/header.svelte';
</script>

<div class="bg-[#F6F3F3]">
    <Head />
    <SideMenu />
    <slot />
</div>
