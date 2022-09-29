<template>
    <label
        class="cookie-comply-switch"
        :title="isRequired ? 'is required' : value"
    >
        <input
            id="value"
            type="checkbox"
            :disabled="isRequired"
            :checked="isRequired || isDefaultEnable"
            :value="value"
            @input="onToggle()"
        >
        <span
            class="cookie-comply-slider cookie-comply-round"
            :class="{
                'cookie-comply-required':
                    isRequired,
            }"
        />
    </label>
</template>
<script>
export default {
    name: 'CookieComplySwitch',
    props: {
        value: {
            type: String,
            required: !0
        },
        isRequired: {
            type: Boolean,
            default: !1
        },
        isDefaultEnable: {
            type: Boolean,
            default: !1
        }
    },
    data: () => ({
        isEnable: !1
    }),
    mounted() {
        (this.isRequired || this.isDefaultEnable) && (this.isEnable = !0, this.$emit('update:checkbox', {
            value: this.value,
            isEnable: !0
        }));
    },
    methods: {
        onToggle(e) {
            this.isEnable = !this.isEnable, this.$emit('update:checkbox', {
                value: e,
                isEnable: this.isEnable
            });
        }
    }
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

.cookie-comply-switch {
	position: relative;
	display: inline-block;
	width: 60px;
	height: 34px;
}
.cookie-comply-switch input {
	opacity: 0;
	width: 0;
	height: 0;
}
.cookie-comply-slider {
	position: absolute;
	cursor: pointer;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	background-color: #ccc;
	-webkit-transition: 0.4s;
	transition: 0.4s;
}
.cookie-comply-slider:before {
	position: absolute;
	content: "";
	height: 26px;
	width: 26px;
	left: 4px;
	bottom: 4px;
	background-color: $color-white;
	-webkit-transition: 0.4s;
	transition: 0.4s;
}
input:checked + .cookie-comply-slider {
	background-color: $color-green;
}
input:focus + .cookie-comply-slider {
	box-shadow: 0 0 1px $color-green;
}
input:checked + .cookie-comply-slider:before {
	-webkit-transform: translateX(26px);
	-ms-transform: translateX(26px);
	transform: translate(26px);
}
.cookie-comply-slider.cookie-comply-round {
	border-radius: 34px;
}
.cookie-comply-slider.cookie-comply-round:before {
	border-radius: 50%;
}
.cookie-comply-required {
	cursor: not-allowed;
}
input:checked + .cookie-comply-required.cookie-comply-slider {
	background-color: #ccc;
}
</style>