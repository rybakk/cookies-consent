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
	data() {
		return {
            showSnackbar: false,
            preferences: [
                {
                    title: 'Analytics',
                    description:
						'Bla bla serviços que podemos oferecer erviços que podemos oferecer erviços que podemos oferecer erviços que podemos oferecer serviços que podemos oferecer.',
                    items: [
                        {
                            label: 'GoogleAnalytics',
                            value: 'ga',
                            isEnable: true,
                        },
                        { label: 'Sentry', value: 'sentry', isEnable: true },
                        { label: 'Mapbox', value: 'mapbox', isEnable: true },
                        {
                            label: 'New Relic',
                            value: 'newRelic',
                            isEnable: true,
                        },
                        { label: 'Dog Food', value: 'dogfood', isEnable: true },
                    ],
                },
            ],
        };
	}
});
</script>

<template>
	<div id="app">
		<cookies-consent :preferences="preferences" />
	</div>
</template>
