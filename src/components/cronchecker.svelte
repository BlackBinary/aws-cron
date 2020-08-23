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
    
    function selectDay(value) {
      const days = ['Monday', 'Thuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
      return days[value];
    }
    
    function selectMonth(value) {
      const months = ['January', 'Februari', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
      return months[value];
    }

    $: timevalue = hour && hour !== '*' ? `At ${formatTime(hour)}:${formatTime(minute)}` : `At minute ${minute}`;
    $: dayvalue = dayOfWeek && dayOfWeek !== '*' ? `on ${selectDay(dayOfWeek)}` : ``;
    $: monthvalue = month && month !== '*' ? `in ${selectMonth(month)}` : ``;

    let type = 'MINUTES';
    function caretPosition(e) {
      let caretPosition = e.target.selectionStart;

      if(caretPosition <= minute.length) {
        type = 'MINUTES';
      } else if (caretPosition >= (minute.length + 1) && caretPosition <= (hour.length + minute.length + 1)) {
        type = 'HOURS';
      } else if (caretPosition >= (hour.length + minute.length + 2) && caretPosition <= (hour.length + minute.length + dayOfWeek.length + 2)) {
        type = 'DAY-OF-WEEK';
      } else if (caretPosition >= (hour.length + minute.length + dayOfWeek.length + 3) && caretPosition <= (hour.length + minute.length + dayOfWeek.length + month.length + 3)) {
        type = 'MONTH';
      } else if (caretPosition >= (hour.length + minute.length + dayOfWeek.length + month.length + 4) && caretPosition <= (hour.length + minute.length + dayOfWeek.length + month.length + dayOfMonth.length + 4)) {
        type = 'DAY-OF-MONTH';
      } else if (caretPosition >= (hour.length + minute.length + dayOfWeek.length + month.length + dayOfMonth.length + 5) && caretPosition <= (hour.length + minute.length + dayOfWeek.length + month.length + dayOfMonth.length + year.length + 5)) {
        type = 'YEAR';
      }
    };

    let specList: array = [
      {
        char: '*',
        desc: 'any value',
        type: ['MINUTES', 'HOURS', 'DAY-OF-WEEK', 'MONTH', 'DAY-OF-MONTH', 'YEAR'],
      },
      {
        char: ',',
        desc: 'value list separator',
        type: ['MINUTES', 'HOURS', 'DAY-OF-WEEK', 'MONTH', 'DAY-OF-MONTH', 'YEAR'],
      },
      {
        char: '-',
        desc: 'range of values',
        type: ['MINUTES', 'HOURS', 'DAY-OF-WEEK', 'MONTH', 'DAY-OF-MONTH', 'YEAR'],
      },
      {
        char: '/',
        desc: 'step values',
        type: ['MINUTES', 'HOURS', 'DAY-OF-WEEK', 'MONTH', 'DAY-OF-MONTH', 'YEAR'],
      },
      {
        char: '0-59',
        desc: 'Allowed Values',
        type: ['MINUTES'],
      },
      {
        char: '0-23',
        desc: 'Allowed Values',
        type: ['HOURS'],
      },
      {
        char: '1-31',
        desc: 'Allowed Values',
        type: ['DAY-OF-MONTH'],
      },
      {
        char: '1-12',
        desc: 'Allowed Values',
        type: ['MONTH'],
      },
      {
        char: 'JAN-DEC',
        desc: 'Alternative Single Values',
        type: ['MONTH'],
      },
      {
        char: '0-6',
        desc: 'Allowed Values',
        type: ['DAY-OF-WEEK'],
      },
      {
        char: 'SUN-SAT',
        desc: 'Alternative Single Values',
        type: ['DAY-OF-WEEK'],
      },
      {
        char: '7',
        desc: 'Sunday (non standard)',
        type: ['DAY-OF-WEEK'],
      },
    ];
</script>

<main>
    <div class="human-readable">{timevalue} {dayvalue} {monthvalue}</div>
    <!-- every minute at {minute}<br>
    every hour at {hour}<br>
    every {dayOfWeek} of the week<br>
    every {month} month<br>
    every {dayOfMonth} of the month<br>
    every {year}th year<br> -->
    <input bind:value={cron} on:keyup={(e) => caretPosition(e)} on:click={(e) => caretPosition(e)}>
    <div class="types">
        <div class="type">
          <span class="{type === 'MINUTES' ? 'active' : ''}">MINUTES</span>
        </div>
        <div class="type">
          <span class="{type === 'HOURS' ? 'active' : ''}">HOURS</span>
        </div>
        <div class="type">
          <span class="{type === 'DAY-OF-WEEK' ? 'active' : ''}">DAY OF WEEK</span>
          
        </div>
        <div class="type">
          <span class="{type === 'MONTH' ? 'active' : ''}">MONTH</span>
        </div>
        <div class="type">
          <span class="{type === 'DAY-OF-MONTH' ? 'active' : ''}"> DAY OF MONTH</span>
        </div>
        <div class="type">
          <span class="{type === 'YEAR' ? 'active' : ''}">YEAR</span>
        </div>
    </div>
    <div class="type-specs">
        <ul>
          {#each specList as item}
            {#if item.type.includes(type)}
              <li>
                <span class="char">{item.char}</span>
                <span class="desc">{item.desc}</span>
              </li>
            {/if}
          {/each}
        </ul> 
    </div>
</main>

<style lang="scss">
* {
  box-sizing: border-box;
}

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

.types {
  display: flex;
  align-items: center;
  justify-content: center;

  .type {
    padding: 0 10px;
    font-size: 10px;
    letter-spacing: 2px;
    .active {
      color:#008080;
      font-weight: bold;
      transition: all 0.2 ease;
    }
  }
}

.type-specs {
  width: 100%;
  max-width: 550px;
  margin: 50px auto;
  box-sizing: border-box;
  font-size: 13px;

  ul {
    list-style: none;
    width: 100%;
    display: block;
    margin: 0;
    padding: 0;

    li {
      display: flex;
      width: 100%;
      line-height: 35px;
      border-bottom: 1px dashed #f1f1f1;

      &:nth-child(odd) {
        background: #f5f5f5;
      }
    }

    .char {
      color: #008080;
      display: block;
      width: 50%;
      padding-right: 15px;
      text-align: right;
    }
    
    .desc {
      display: block;
      width: 50%;
      padding-left: 15px;
      text-align: left;
    }
  }  
}

.human-readable {
  display: block; 
  margin-bottom: 20px;
  font-size: 30px;
}

</style>