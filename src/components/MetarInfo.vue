<template>
	<div>
		<h4>Here is the current METAR for KHSD</h4>
		<p>{{ this.rawMetar }}</p>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: "metar-info",

	data: () => ({
		rawMetar: null,
		metar: {},
		icaoCode: null,
		axiosOptions: {
			headers: { "X-API-Key": "f419ee367c914e7b94134a009f" },
		},
		errors: [],
	}),

	created() {
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
};
</script>

<style lang="scss" scoped></style>
