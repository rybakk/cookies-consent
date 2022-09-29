<script>
import Vue from "vue";
// Uncomment import and local "components" registration if library is not registered globally.
// import { CookiesConsentSample } from '@/entry.esm';
import { CookiesConsent } from "@/entry.esm";

export default Vue.extend({
	name: "ServeDev",
	components: {
		CookiesConsent,
	},
});
</script>

<template>
	<div id="app">
		<cookies-consent />
	</div>
</template>
