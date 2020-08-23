<script lang="ts">
	import Header from './components/header.svelte';
	import CronChecker from './components/cronchecker.svelte';
import Cronchecker from './components/cronchecker.svelte';
</script>

<main>
	<div class="wrapper">
		<Header />
		<!-- <div class="box header">
			Hi
		</div> -->
		<div class="box sidebar">Sidebar</div>
		<div class="box content">
			<Cronchecker />
		</div>
		<div class="box footer">Footer</div>
	</div>
</main>

<style global lang="scss">
	@import './styles/grid';
</style>