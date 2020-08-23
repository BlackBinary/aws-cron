<script lang="ts">
	import Header from './components/header.svelte';
	import CronChecker from './components/cronchecker.svelte';
import Cronchecker from './components/cronchecker.svelte';
</script>

<main>
	<div class="wrapper">
		<Header />
		<div class="box content">
			<Cronchecker />
		</div>
		<div class="box footer">C-ron & D-velop</div>
	</div>
</main>

<style global lang="scss">
  @import './styles/grid';
  
  .footer {
    text-align: center;
    font-size: 10px;
    font-style: italic;
  }
</style>