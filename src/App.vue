/* eslint-disable no-console */
<template>
	<v-app>
		<v-main>
			<MetarInfo />
		</v-main>
	</v-app>
</template>

<script>
import MetarInfo from "./components/MetarInfo";

export default {
	name: "App",

	components: {
		MetarInfo,
	},

	data: () => ({}),
};
</script>
