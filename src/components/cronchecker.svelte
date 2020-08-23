<script lang="ts">
import { create_out_transition } from "svelte/internal";


    let cron: string = '* * * * * *';

    $: [
        minute,
        hour,
        dayOfWeek,
        month,
        dayOfMonth,
    ] = cron.split(' ');
</script>

<main>
    every minute at {minute}<br>
    every hour at {hour}<br>
    every {dayOfWeek} of the week<br>
    every {month} month<br>
    every {dayOfMonth} of the month<br>
    <input bind:value={cron}>
</main>

<style lang="scss">
 main {
   text-align: center;
 }
</style>