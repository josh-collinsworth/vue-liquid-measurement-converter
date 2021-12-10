<template>
  <div id="app">
		<PWAPrompt />
    <MeasurementsTable />
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
	grid-template-columns: 100%;
}

#app {
	width: 100%;
}

#lm {
	margin: auto;
	width: 100%;
	max-width: 24rem;
	padding: 1rem;

	span {
		text-align: center;
		font-size: 1.25rem;
		display: flex;
		align-items: center;
		color: var(--lightGray);
		margin-bottom: 0.3em;
		left: 0;
	}

	sup {
		float: right;
		margin-right: -1ch;
		padding-top: .1em;
	}

	.footnote {
		margin-top: 1rem;
		font-size: .75rem;
	}

	.card {
		display: grid;
		border-radius: 0.25rem;
		align-items: center;

		&:first-of-type {
			margin-bottom: 2rem;

			.flex-group {
				padding-bottom: 0.5rem;
				border-bottom: 1px solid currentColor;
				position: relative;

				&::after {
					content: '';
					width: 0.5rem;
					height: 0.5rem;
					background: currentColor;	
					position: absolute;
					left: calc(50% - 0.25rem);
					bottom: -.25rem;
					transform: rotate(135deg);
					clip-path: polygon(0 0, 100% 100%, 100% 0%);
				}
			}
		}

		h2 {
			font-size: 2rem;
			font-weight: bold;
			text-align: center;
			margin: 0 0 1em;
		}

		select,
		input {
			font-size: 1rem;
		}

		select {
			padding: 0.25rem 0.5rem;
			border-radius: .25rem;
		}

		.flex-group {
			display: grid;
			align-items: baseline;
			justify-content: space-between;
			grid-template-columns: 1fr max-content;
			grid-template-rows: 1fr;
			border-bottom: 1px solid var(--lightGray);

			label {
				text-align: right;
				font-size: 1.25rem;
				position: relative;
			}
		}

		.number,
		input {
			font-family: "Martel";
			border: none;
			text-align: left;
			display: inline-block;
			font-size: 1.25rem;
			background: transparent;
			width: 60vw;
			box-shadow: none;
			color: inherit;

			@media (min-width: 440px) {
				width: auto;
			}

			&:focus + label {
				color: var(--yellow);
			}
		}

		.number {
			margin: .25rem 0;
		}
	}
}
</style>
