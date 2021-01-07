<template>
	<v-container fluid>
		<v-form ref="form" v-model="valid" lazy-validation
			>>
			<v-row>
				<v-col class="mt-4" offset-md="4" cols="3">
					<v-text-field
						v-model="icaoCode"
						:counter="4"
						:rules="icaoRules"
						label="Please Enter ICAO Code"
						required
					></v-text-field>
				</v-col>
				<v-col>
					<v-btn
						:disabled="!valid"
						color="primary"
						class="ml-4 mt-11"
						outlined
						@click="getMetar"
					>
						Get METAR
					</v-btn>
				</v-col>
			</v-row>
		</v-form>
		<v-row>
			<v-col>
				<v-card class="mx-auto my-6" max-width="750">
					<v-card-title> KHSD </v-card-title>
					<v-card-subtitle>
						Current METAR for Sundance Airport
					</v-card-subtitle>
					<v-divider class="mx-4"></v-divider>
					<v-card-text>
						{{ this.rawMetar }}
					</v-card-text>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
import axios from "axios";

export default {
	name: "metar-info",

	data: () => ({
		rawMetar: "KHSD 051755Z AUTO 16011KT 10SM CLR 11/03 A3007 RMK A01",
		metar: {},
		icaoCode: null,
		axiosOptions: {
			headers: { "X-API-Key": "f419ee367c914e7b94134a009f" },
		},
		errors: [],
		icaoRules: [
			(v) => !!v || "ICAO code is required",
			(v) =>
				(v && v.length > 3 && v.length < 5) ||
				"ICAO code must be 4 characters",
		],
		valid: false,
	}),

	created() {},

	methods: {
		getMetar: () => {
			axios
				.get(
					"https://api.checkwx.com/metar/KHSD/decoded",
					this.axiosOptions
				)
				.then((response) => {
					let resp = response.data;
					this.metar = resp.data[0];
					this.rawMetar = this.metar.raw_text;
					// eslint-disable-next-line no-console
					console.log(this.metar);
				})
				.catch((e) => {
					this.errors.push(e);
				});
		},
	},
};
</script>

<style lang="scss" scoped></style>
