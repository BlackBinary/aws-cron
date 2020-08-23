<script lang="ts">
    let cron: string = '* * * * * *';

    $: minute = cron.split(" ")[0];
    $: hour = cron.split(" ")[1];
    $: dayOfWeek = cron.split(" ")[2];
    $: month = cron.split(" ")[3];
    $: dayOfMonth = cron.split(" ")[4];
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