<script setup>
import { computed, ref } from 'vue';
import { cva } from "class-variance-authority";
import Loading from '../Loading.vue';

const props = defineProps({
    intent: 
    {
        type: String,
        validator(value)
        {
            return ["primary", "secondary", "tertiary", "info", "success", "danger", "warning"].includes(value);
        },
        default: "info",
    },
    as: {
        type: [ String, Object ],
        default: "button"
    },
    icon: {
        type: [ String, Object ],
        default: "left"
    },
    leftIcon: Object,
    rightIcon: Object,
    loading: Boolean,
    disabled: Boolean,
    action: Function,
});

const buttonClass = computed(() => 
{
    return cva("button", 
    {
        variants: 
        {
            intent: 
            {       
                primary: "primary",
                secondary: "secondary", 
                tertiary: "tertiary",
                info: "info", 
                success: "success", 
                danger: "danger", 
                warning: "warning"
            },
            disabled: 
            {
                true: "disabled",
                
            }
        }
    })(
    {
        intent: props.intent,
        disabled: props.disabled
    });
});
</script>

<template>
    <component :class="buttonClass" :disabled="props.disabled" :is="props.as">
        <Loading :loading="props.loading" />
        <component :is="props.leftIcon" :class="['button-icon', 'left']" v-if="!props.loading" />
        <span :class="[props.loading && 'hidden']">
            <slot />
        </span>
        <component :is="props.rightIcon" :class="['button-icon', 'right']" v-if="!props.loading" />
    </component>
</template>