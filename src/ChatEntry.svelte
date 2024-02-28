<script lang="ts">
import type ChatEntryModel from './ChatEntryModel';

export let model: ChatEntryModel;
</script>

<div>
<div>The prompt is: {model.prompt} </div>
<div>The response is: {model.response} </div>
</div>