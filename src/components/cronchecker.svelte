<script lang="ts">
    let cron: string = '* * * * * *';

    $: splitted = cron.split(" ");
    $: minute = splitted[0];
    $: hour = splitted[1];
    $: dayOfWeek = splitted[2];
    $: month = splitted[3];
    $: dayOfMonth = splitted[4];
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