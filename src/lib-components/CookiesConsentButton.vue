<template>
    <button
        @click="handleClick"
        class="cookie-comply__button"
        :class="[className]"
    >
        <slot />
    </button>
</template>
<script>
export default {
    name: 'CookieComplyButton',
    props: {
        className: {
            type: String,
            required: !1,
            default: ''
        }
    },
    emits: ['handleClick'],
    methods: {
        handleClick() {
            this.$emit('handleClick');
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
    

.cookie-comply__button {
	padding: 12px 32px;
	border: 1px solid #333;
	background-color: $color-white;
	font-weight: 600;
	font-size: 1rem;
	border-radius: 5px;
	cursor: pointer;
}
.cookie-comply__button-accept {
    background-color: $color-green;
    color: $color-white;
    border: none;
}
</style>