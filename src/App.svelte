<script lang="ts">
	import Header from './components/header.svelte';
	import CronChecker from './components/cronchecker.svelte';
</script>

<main>
	<div class="wrapper">
		<Header />
		<!-- <div class="box header">
			Hi
		</div> -->
		<div class="box sidebar">Sidebar</div>
		<div class="box content">Content
			<br /> More content than we had before so this column is now quite tall.</div>
		<div class="box footer">Footer</div>
	</div>
	<!-- <Header/>
	<CronChecker/> -->
</main>

<style global lang="scss">
	@import './styles/grid';
</style>