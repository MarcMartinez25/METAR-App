<template>
	<v-container fluid>
		<v-card class="mx-auto my-12" max-width="750">
			<v-card-title>
				KHSD
			</v-card-title>
			<v-card-subtitle>
				Current METAR for Sundance Airport
			</v-card-subtitle>
			<v-divider class="mx-4"></v-divider>
			<v-card-text>
				{{ this.rawMetar }}
			</v-card-text>
		</v-card>
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
