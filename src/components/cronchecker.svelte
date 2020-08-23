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
    <div class="types">
        <div class="type">
          MINUTES
        </div>
        <div class="type">
          HOURS
        </div>
        <div class="type">
          DAY OF WEEK
        </div>
        <div class="type">
          MONTH
        </div>
        <div class="type">
          DAY OF MONTH
        </div>
        <div class="type">
          YEAR
        </div>
    </div>
</main>

<style lang="scss">
main {
  text-align: center;
}

input {
  border-radius: 50px;
  line-height: 70px;
  font-size: 30px;
  padding: 0 30px;
  letter-spacing: 3px;
  text-align: center;
  outline: none;
  color: #aeaeae;
}
</style>