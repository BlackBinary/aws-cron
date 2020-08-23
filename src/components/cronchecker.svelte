<script lang="ts">
    let cron: string = '* * * * * *';
</script>

<main>
    every day at {cron}<br>
    <input bind:value={cron}>
</main>

<style lang="scss">
 main {
   text-align: center;
 }
</style>