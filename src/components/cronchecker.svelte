<script lang="ts">
    let cron: string = '* * * * * *';

    $: minute = cron.charAt(0);
    $: hour = cron.charAt(2);
    $: dayOfWeek = cron.charAt(4);
    $: month = cron.charAt(6);
    $: dayOfMonth = cron.charAt(8);
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