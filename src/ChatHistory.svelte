<script lang="ts">
    import ChatEntry from "./ChatEntry.svelte";
    import {entries} from "./store";
</script>

<div>
    {#each $entries as entry}
        <ChatEntry model={entry} />
        <hr>
    {/each}
</div>
