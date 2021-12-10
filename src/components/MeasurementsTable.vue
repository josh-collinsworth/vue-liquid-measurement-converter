<template>
  <div id="lm">

		
	<div class="card">
		<div class="flex-group">
			<input v-model="absoluteUnit" type="number">

			<select v-model="unit">
				<option value="0.16666666">TSP</option>
				<option value="0.03381402">ML</option>
				<option value="0.5">TBSP</option>
				<option value="1">Ounce</option>
				<option value="8">Cup</option>
				<option value="16">Pint</option>
				<option value="32">Quart</option>
				<option value="33.8140225">Liter</option>
				<option value="128">Gallon</option>
			</select>
		</div>
	</div>



	<div class="card">
		<div class="flex-group">
			<span class="number">{{ ml }}</span>
			<label for="ml">
				ml<sup>*</sup>
			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ tsp }}</span>
			<label for="tsp">
				tsp
			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ tbsp }}</span>
			<label for="tbsp">
				tbsp
			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ ounce }}</span>
			<label for="oz">
				oz
			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ cup }}</span>
			<label for="cup">
				cup{{ cup != 1 ? 's' : '' }}
			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ pint }}</span>
			<label for="pint">
				pint{{ pint != 1 ? 's' : '' }}

			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ quart }}</span>
			<label for="quart">
				quart{{ quart != 1 ? 's' : '' }}
			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ liter }}</span>
			<label for="liter">
				liter{{ liter != 1 ? 's' : '' }}<sup>*</sup>
			</label>
		</div>
	</div>

	<div class="card">
		<div class="flex-group">
			<span class="number">{{ gallon }}</span>
			<label for="gallon">
				gallon{{ gallon != 1 ? 's' : '' }}
			</label>
		</div>
	</div>

	<div class="card footnote">
		* Rounded; not exact
	</div>
</div>
</template>

<script>
export default {
  name: 'MeasurementsTable',
  data: () => ({
		unit: 1,
		absoluteUnit: 1,
		oz: 32 //Ounces are the only true data value here every other value is a dependent computed property that multiplies or divides ounces
	}),

	methods: {
		//Does some nice formatting on the number, if it's a decimal, to make it a little more readable and limit it to 10 total characters
		format(num) {
			num = Number(num)
			return parseInt(num) === num ? num : num.toString().substring(0, 10)
		}
	},

	computed: {
		ml() {
			return parseInt(this.format(this.absoluteUnit * this.unit * 29.57352968750042))
		},

		tsp() {
			return this.format(this.absoluteUnit * this.unit * 6)
		},

		tbsp() {
			return this.format(this.absoluteUnit * this.unit * 2)
		},

		ounce() {
			return this.format(this.absoluteUnit * this.unit)
		},

		cup() {
			return this.format(this.absoluteUnit * this.unit / 8)
		},

		pint() {
			return this.format(this.absoluteUnit * this.unit / 16)
		},

		quart() {
			return this.format(this.absoluteUnit * this.unit / 32)
		},

		liter() {
			return this.format(this.absoluteUnit * this.unit * 0.02957352968750042.toFixed(2))
		},

		gallon() {
			return this.format(this.absoluteUnit * this.unit / 128)
		},
	}
}
</script>

