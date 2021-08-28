<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    let searchTerm = '';
    const search = (e) => {
        searchTerm = event.target.value;
        if (searchTerm) {
            dispatch('search', {
                searchTerm,
            });
        } else {
            dispatch('clearSearch', {});
        }
    };
</script>

<input
    type="text"
    placeholder="search your movies"
    value={searchTerm}
    on:keyup={search}
/>

<style>
    input {
        width: 100%;
    }
</style>
