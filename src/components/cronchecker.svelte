<script lang="ts">
    let cron: string = '* * * * * *';

    let minute: number = cron.charAt(0);
    let hour: number = cron.charAt(2);
    let dayOfWeek: number = cron.charAt(4);
    let month: number = cron.charAt(6);
    let dayOfMonth: number = cron.charAt(8);
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
    
</style>