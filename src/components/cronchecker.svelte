<script lang="ts">
    let cron: string = '* * * * * *';

    $: [
        minute,
        hour,
        dayOfWeek,
        month,
        dayOfMonth,
        year,
    ] = cron.split(' ');

    function formatTime(value) {
        return (`0${value}`).slice(-2);
    }

    $: timevalue = hour && hour !== '*' ? `At ${formatTime(hour)}:${formatTime(minute)}` : `At minute ${minute}`;
</script>

<main>
    {timevalue}<br>`
    every minute at {minute}<br>
    every hour at {hour}<br>
    every {dayOfWeek} of the week<br>
    every {month} month<br>
    every {dayOfMonth} of the month<br>
    every {year}th year<br>
    <input bind:value={cron}>
</main>

<style lang="scss">
main {
text-align: center;
}
</style>