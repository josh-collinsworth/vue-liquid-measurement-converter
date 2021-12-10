<template>
  <div id="app">
		<PWAPrompt />
    <MeasurementsTable />
		<footer>
			<div class="container">
				Made by <a href="https://joshcollinsworth.com">Josh Collinsworth</a>
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
	--white: #ffffff;
	--orange: #ff6a13;
	--yellow: #ffd100;
	--lightGray: #a7a8aa;
	--darkGray: #53565a;
	--lightBlue: #7ba7bc;
	--darkBlue: #34657f;
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
	outline: none;
	background-color: var(--yellow);
}

*::selection {
	background: var(--yellow);
}

html {
	font-size: 1.125em;
}

body {
	margin: 0;
	font-family: "Barlow Condensed", sans-serif;
	background: #f4f4f4;
	color: var(--darkGray);
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
	background: var(--darkBlue);
	color: var(--white);
	position: sticky;
	top: 100vh;
	font-size: 0.75rem;
}
</style>
