<template>
  <div id="app">
		<PWAPrompt />
    <MeasurementsTable />
		<footer>
			<div class="container">
				Made by <a href="https://joshcollinsworth.com">Josh Collinsworth</a>&emsp;|&emsp;<a href="https://github.com/josh-collinsworth/vue-liquid-measurement-converter">GitHub repo</a>
			</div>
		</footer>
  </div>
</template>

<script>
import MeasurementsTable from './components/MeasurementsTable.vue'
import PWAPrompt from './components/PWAPrompt.vue'

export default {
  name: 'App',
  components: {
    MeasurementsTable,
    PWAPrompt
  }
}
</script>

<style lang="scss">
:root {
	--background: #e0fbfc;
	--bright: #ee6c4d;
	--dark: #3d5a80;
	--darker: #293241;
	--accent: #98c1d9;
}

*,
*:before,
*:after {
	box-sizing: border-box;
	font-family: inherit;
	color: inherit;
	max-width: 100%;
}

*:focus {
	outline: 2px solid var(--bright);
	outline-offset: 2px;
}

*::selection {
	background: var(--accent);
	color: var(--dark);
}

html {
	font-size: 1.125em;
}

body {
	margin: 0;
	font-family: "Barlow Condensed", sans-serif;
	background: var(--background);
	color: var(--dark);
	min-height: 100vh;
	display: grid;
	place-content: center;
	grid-template-columns: 100%;
	min-height: 100vh;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}

#app {
	width: 100%;
	min-height: 100vh;
}

.container {
	margin: 0 auto;
	width: 100%;
	max-width: 24rem;
}

footer {
	padding: 0.75rem 1.5rem;
	background: var(--dark);
	color: var(--background);
	position: sticky;
	top: 100vh;
	font-size: 0.75rem;

	*:focus {
		outline-color: var(--accent);
	}
}
</style>
