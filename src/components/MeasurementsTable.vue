<template>
  <div id="lm">

	<span>
		<!-- Empty span here to make the grid line up properly --></span>

	<div class="card">
		<div class="flex-group">
			<input v-model="ml" type="number" id="ml">
			<label for="ml">
				ml
			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="tsp" type="number" id="tsp">
			<label for="tsp">
				tsp
			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="tbsp" type="number" id="tbsp">
			<label for="tbsp">
				tbsp
			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="ounce" type="number" id="oz">
			<label for="oz">
				oz
			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="cup" type="number" id="cup">
			<label for="cup">
				cup{{ cup != 1 ? 's' : '' }}
			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="pint" type="number" id="pint">
			<label for="pint">
				pint{{ pint != 1 ? 's' : '' }}

			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="quart" type="number" id="quart">
			<label for="quart">
				quart{{ quart != 1 ? 's' : '' }}
			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="liter" type="number" id="liter">
			<label for="liter">
				liter{{ liter != 1 ? 's' : '' }}
			</label>
		</div>
	</div>

	<span> = </span>

	<div class="card">
		<div class="flex-group">
			<input v-model="gallon" type="number" id="gallon">
			<label for="gallon">
				gallon{{ gallon != 1 ? 's' : '' }}
			</label>
		</div>
	</div>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
		//Ounces are the only true data value here; every other value is a dependent computed property that multiplies or divides ounces
		oz: 32
	}),

	methods: {
		//Does some nice formatting on the number, if it's a decimal, to make it a little more readable and limit it to 10 total characters
		format(num) {
			num = Number(num);
			return parseInt(num) === num ? num : num.toString().substring(0, 10);
		}
	},

	computed: {
		tsp: {
			get() {
				return this.format(this.oz * 6);
			},
			set(val) {
				this.oz = val / 6;
			}
		},
		ml: {
			get() {
				return parseInt(this.format(this.oz * 29.57352968750042));
			},
			set(val) {
				this.oz = val / 29.57352968750042;
			}
		},
		tbsp: {
			get() {
				return this.format(this.oz * 2);
			},
			set(val) {
				this.oz = val / 2;
			}
		},
		ounce: {
			get() {
				return this.format(this.oz);
			},
			set(val) {
				this.oz = val;
			}
		},
		cup: {
			get() {
				return this.format(this.oz / 8);
			},
			set(val) {
				this.oz = val * 8;
			}
		},
		pint: {
			get() {
				return this.format(this.oz / 16);
			},
			set(val) {
				this.oz = val * 16;
			}
		},
		quart: {
			get() {
				return this.format(this.oz / 32);
			},
			set(val) {
				this.oz = val * 32;
			}
		},
		liter: {
			get() {
				return Number(this.format(this.oz * 0.02957352968750042)).toFixed(2);
			},
			set(val) {
				this.oz = val / 0.02957352968750042;
			}
		},
		gallon: {
			get() {
				return this.format(this.oz / 128);
			},
			set(val) {
				this.oz = val * 128;
			}
		}
	}
}
</script>

