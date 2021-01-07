/* eslint-disable no-console */
<template>
	<v-app>
		<v-main>
			<v-app-bar color="primary" dark>
				<v-toolbar-title>Metar Data</v-toolbar-title>
				<v-spacer></v-spacer>
				<v-btn icon>
					<v-icon>fas fa-into</v-icon>
				</v-btn>
			</v-app-bar>
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
