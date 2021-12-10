<template>
  <div id="app">
		<PWAPrompt />
    <MeasurementsTable msg="Welcome to Your Vue.js App"/>
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
@import url("https://fonts.googleapis.com/css?family=Barlow+Condensed:300&display=swap");
@import url("https://fonts.googleapis.com/css?family=Martel&display=swap");

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
	font-family: "Barlow Condensed";
	background: #eee;
	color: var(--darkGray);
	min-height: 100vh;
	display: grid;
	place-content: center;
}

#lm {
	display: grid;
	margin: auto;
	max-width: 24rem;
	grid-template-columns: 0.8rem minmax(12rem, 20rem);
	grid-gap: 1rem;
	padding: 1rem;

	@media (min-width: 800px) {
		transform: skewX(29deg);

		span,
		.card {
			transform: skewX(-29deg);
		}
	}

	span {
		text-align: center;
		font-size: 1.25rem;
		display: flex;
		align-items: center;
		color: var(--lightGray);
		margin-bottom: 0.3em;
		left: 0;
	}

	.card {
		display: grid;
		border-radius: 0.25rem;
		align-items: center;

		h2 {
			font-size: 2rem;
			font-weight: bold;
			text-align: center;
			margin: 0 0 1em;
		}

		.flex-group {
			display: grid;
			align-items: baseline;
			justify-content: space-between;
			grid-template-columns: 1fr max-content;
			grid-template-rows: 1fr;
			border-bottom: 1px solid;

			label {
				text-align: right;
				font-size: 1.25rem;
				position: relative;
			}

			input {
				font-family: "Martel";
				border: none;
				text-align: left;
				display: inline-block;
				font-size: 1.25rem;
				background: transparent;
				width: 60vw;
				box-shadow: none;

				@media (min-width: 440px) {
					width: auto;
				}

				&:focus + label {
					color: var(--yellow);
				}
			}
		}
	}
}
</style>
