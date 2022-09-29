<template>
    <div v-sticky sticky-side="bottom">
        <aside class="cookie-comply">
            <div class="cookie-comply__header">
                <h3 class="cookie-comply__header-title">
                    {{ headerTitle || "Cookie settings" }}
                </h3>
                <p class="cookie-comply__header-description">
                    {{
                        headerDescription ||
                            "We use cookies and similar technologies to help personalize content and offer a better experience. You can opt to customize them by clicking the preferences button."
                    }}
                </p>
            </div>
            <div class="cookie-comply__actions">
                <cookies-consent-button @handleClick="openPreferences">
                    {{ preferencesLabel }}
                </cookies-consent-button>
                <cookies-consent-button
                    :class-name="'cookie-comply__button-accept'"
                    @handleClick="handleAcceptAll"
                >
                    {{ acceptAllLabel }}
                </cookies-consent-button>
            </div>
        </aside>
        <cookies-consent-modal
            :preferences="preferences"
            v-if="isModalOpen"
            @cookie-comply-close="isModalOpen = false"
            @cookie-comply-save="onSave"
        />
    </div>
</template>
<script>
import CookiesConsentModal from './CookiesConsentModal.vue';
import CookiesConsentButton from './CookiesConsentButton.vue';
export default {
    name: 'CookieComply',
    components: {
        CookiesConsentButton,
        CookiesConsentModal,
    },
    props: {
        headerTitle: {
            type: String,
            default: 'Cookie settings',
        },
        headerDescription: {
            type: String,
            default:
				'We use cookies and similar technologies to help personalize content and offer a better experience. You can opt to customize them by clicking the preferences button.',
        },
        preferencesLabel: {
            type: String,
            default: 'Preferences',
        },
        acceptAllLabel: {
            type: String,
            default: 'Accept All',
        },
        preferences: {
            type: Array,
            default: () => [],
        },
        target: {
            type: String,
            default: 'body',
        },
    },
    data: () => ({
        showCookieComply: !0,
        isModalOpen: !1,
    }),
    mounted() {
        localStorage.getItem('cookies-accepted') && (this.showCookieComply = !1);
    },
    methods: {
        handleAcceptAll() {
            (this.showCookieComply = !1),
            localStorage.setItem('cookies-accepted', 'all'),
            this.$emit('on-accept-all-cookies');
        },
        openPreferences() {
            this.isModalOpen = !0;
        },
        onSave(e) {
            (this.isModalOpen = !1), (this.showCookieComply = !1);
            const o = Object.values(e);
            localStorage.setItem('cookies-accepted', JSON.stringify(o)),
            this.$emit('on-save-cookie-preferences', o);
        },
    },
};
</script>

<style lang="scss" scoped>
$spacing-sm: 8px;
$spacing-md: 14px;
$spacing-lg: 20px;
$color-green: #00c58e;
$color-white: #ffffff;
$box-shadow: 0 1px 6px 1px rgba(0, 0, 0, 0.1), 0 1px 7px 1px rgba(0, 0, 0, 0.6);
$border-radius: 8px;
$background-overlay: rgba(34, 34, 34, 0.3);
$border-color-lightest: 1px solid rgba(200, 200, 200, 0.2);
$border-color-light: 1px solid rgba(0, 0, 0, 0.1);

.cookie-comply {
	display: grid;
	grid-gap: $spacing-lg;
	grid-template-columns: 1fr minmax(35%, 40%);
	position: absolute;
	bottom: $spacing-sm;
	left: $spacing-sm;
	right: $spacing-sm;
	background-color: $color-white;
	box-shadow: $box-shadow;
	padding: $spacing-md;
	border-radius: $border-radius;
}
@media (max-width: 1024px) {
	.cookie-comply {
		grid-template-columns: none;
	}
}

.cookie-comply__header {
	justify-self: flex-start;
	text-align: initial;
}
.cookie-comply__header-title,
.cookie-comply__header-description {
	margin: 0;
}
.cookie-comply__header-title {
	margin-bottom: $spacing-sm;
}
.cookie-comply__header-description {
	line-height: 20px;
}
.cookie-comply__actions {
	display: grid;
	grid-gap: $spacing-lg;
	grid-template-columns: repeat(2, 1fr);
	align-self: center;
}
@media (max-width: 480px) {
	.cookie-comply__header {
		margin-bottom: $spacing-sm;
	}
	.cookie-comply__actions {
		grid-template-columns: auto;
	}
}
</style>