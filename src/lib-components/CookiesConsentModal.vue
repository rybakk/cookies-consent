<template>
    <div class="cookie-comply__modal">
        <div class="cookie-comply__modal-middle">
            <div class="cookie-comply__modal-inner">
                <img
                    @click="onCloseModal"
                    alt="Back arrow"
                    src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjE2cHgiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2cHgiIGZpbGw9IiMwMDAwMDAiPjxyZWN0IGZpbGw9Im5vbmUiIGhlaWdodD0iMTYiIHdpZHRoPSIxNiIvPjxnPjxwb2x5Z29uIHBvaW50cz0iMTcuNzcsMy43NyAxNiwyIDYsMTIgMTYsMjIgMTcuNzcsMjAuMjMgOS41NCwxMiIvPjwvZz48L3N2Zz4="
                    class="cookie-comply__back-arrow"
                >
                <header class="cookie-comply__modal-header">
                    <h3>{{ titleLabel }}</h3>
                </header>
                <main class="cookie-comply__modal-content">
                    <div
                        v-for="(preference, index) in preferences"
                        :key="'pref_' + index"
                    >
                        <h2>{{ preference.title }}</h2>
                        <p>
                            {{ preference.description }}
                        </p>
                        <div
                            class="cookie-comply__modal-switches"
                            v-for="(item, i) in preference.items"
                            :key="'item_' + i"
                        >
                            <h3>{{ item.label }}</h3>
                            <cookies-consent-switch :value="item.value" :is-required="item.isRequired" :is-default-enable="item.isEnable" @update:checkbox="handleCheckboxUpdate" />
                        </div>
                    </div>
                </main>
                <div class="cookie-comply__modal-footer">
                    <cookies-consent-button @handleClick="onSaveConfiguration">
                        {{ saveLabel }}
                    </cookies-consent-button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import CookiesConsentButton from './CookiesConsentButton.vue';
import CookiesConsentSwitch from './CookiesConsentSwitch.vue';
export default {
    name: 'CookieComplyModal',
    components: {
        CookiesConsentButton,
        CookiesConsentSwitch
    },
    props: {
        preferences: {
            type: Array,
            default: () => [],
        },
        saveLabel: {
            type: String,
            default: 'Save'
        },
        titleLabel: {
            type: String,
            default: 'Your privacy preferences'
        },
    },
    data: () => ({
        checkedValues: [],
    }),
    methods: {
        handleCheckboxUpdate({ value: e, isEnable: o }) {
            o
                ? this.checkedValues.push(e)
                : this.checkedValues.splice(this.checkedValues.indexOf(e), 1);
        },
        onSaveConfiguration() {
            this.$emit('cookie-comply-save', this.checkedValues);
        },
        onCloseModal() {
            this.$emit('cookie-comply-close');
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

.cookie-comply__modal {
	display: table;
	position: fixed;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	height: 100%;
	width: 100%;
	background-color: $background-overlay;
	header {
		h3 {
			text-align: center;
		}
	}
}
.cookie-comply__modal-middle {
	display: table-cell;
	vertical-align: middle;
}
.cookie-comply__modal-inner {
	position: relative;
	margin-left: auto;
	margin-right: auto;
	width: 400px;
	padding: $spacing-lg;
	background-color: $color-white;
	border-radius: $spacing-sm;
	box-shadow: $box-shadow;
}
.cookie-comply__back-arrow {
	position: absolute;
	left: $spacing-lg;
	cursor: pointer;
}
.cookie-comply__modal-content {
	overflow-y: scroll;
	max-height: 400px;
	text-align: left;
}
.cookie-comply__modal-switches {
	display: flex;
	justify-content: space-between;
	align-items: center;
	border-bottom: $border-color-lightest;
}
@media (max-width: 480px) {
	.cookie-comply__modal-middle {
		padding: $spacing-md;
	}
	.cookie-comply__modal-inner {
		width: auto;
	}
}
.cookie-comply__modal-header {
	border-bottom: $border-color-light;
}
.cookie-comply__modal-footer {
	border-top: $border-color-light;
	padding-top: $spacing-lg;
}
</style>