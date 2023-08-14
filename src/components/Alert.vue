<script setup>
import { computed } from 'vue';
import { InformationCircleIcon, XMarkIcon, CheckCircleIcon, ExclamationTriangleIcon, XCircleIcon } from "@heroicons/vue/20/solid/index.js";
import { cva } from "class-variance-authority";

const props = defineProps(
{
    title: String,
    intent: 
    {
        type: String,
        validator(value)
        {
            return ["info", "success", "danger", "warning"].includes(value);
        },
        default: "info",
    },
    show: 
    {
        type: Boolean,
        default: true,
    },
    onDismiss: Function,
});

const containerClass = computed(() => 
{
    return cva("alert", 
    {
        variants: 
        {
            intent: 
            {
                info: "bg-blue-100",
                success: "bg-green-100",
                warning: "bg-orange-100",
                danger: "bg-red-100",
            },
        },
    })({
        intent: props.intent,
    });
});

const iconClass = computed(() => 
{
    return cva("alert-icon", 
    {
        variants: 
        {
            intent: 
            {
                info: "text-blue-800",
                success: "text-green-800",
                warning: "text-orange-800",
                danger: "text-red-800",
            },
        },
    })({
        intent: props.intent,
    });
});

const iconComponent = computed(() => 
{
    const icons = 
    {
        success: CheckCircleIcon,
        warning: ExclamationTriangleIcon,
        danger: XCircleIcon,
        info: InformationCircleIcon,
    };

    return icons[props.intent];
});

const closeButtonClass = computed(() => 
{
    return cva("alert-close", 
    {
        variants: 
        {
            intent: 
            {
                info: "text-blue-900 hover:bg-blue-200",
                success: "text-green-900 hover:bg-green-200",
                warning: "text-orange-900 hover:bg-orange-200",
                danger: "text-red-900 hover:bg-red-200",
            },
        },
    })({
        intent: props.intent,
    });
});

const titleClass = computed(() => 
{
    return cva("alert-title", 
    {
        variants: 
        {
            intent: 
            {
                info: "info",
                success: "success",
                warning: "warning",
                danger: "danger",
            },
        },
    })({
        intent: props.intent,
    });
});

const contentClass = computed(() => 
{
    return cva("alert-content", 
    {
        variants: 
        {
            intent: 
            {
                info: "info",
                success: "success",
                warning: "warning",
                danger: "danger",
            },
        },
    })({
        intent: props.intent,
    });
});

/**
*   Cette fonction permet de fermer l'alerte.
**/
function dismiss() 
{
    if (props.onDismiss) 
    {
        props.onDismiss();
    }
}
</script>

<template>
    <transition leave-active-class="duration-300" leave-to-class="opacity-0">
        <div :class="containerClass" v-if="props.show">
            <div class="alert-icons">
                <component :is="iconComponent" :class="iconClass" />
            </div>
            <div class="alert-container">
                <h2 :class="titleClass">{{ props.title }}</h2>
                <div :class="contentClass">
                    <slot />
                </div>
            </div>
            <div class="alert-buttons" v-if="props.onDismiss">
                <button id="close" name="close" @click="dismiss()" :class="closeButtonClass">
                    <XMarkIcon :class="iconClass"/>
                </button>
            </div>
        </div>
    </transition>
</template>