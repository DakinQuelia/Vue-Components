<script setup>
import { computed, provide } from "vue";
import { v4 as uuid } from "uuid";
import { cva } from "class-variance-authority";
import Label from './Label.vue';

const props = defineProps(
{
    id: 
    {
        type: String,
        default: () => `field-${uuid()}`,
    },
    as: {
        type: [ String, Object ],
        default: "input"
    },
    type: String,
    disabled: Boolean,
    label: String,
    required: Boolean,
    placeholder: String,
    error: String,
    help: String,
});

const ariaDescribedBy = computed(() => 
{
    return !!props.help ? `help-${uuid()}` : null;
});

const fieldClass = computed(() => 
{
    return cva("input-control", 
    {
        variants: 
        {
            intent: 
            {       

            },
            disabled: 
            {
                true: "disabled",
            }
        }
    })(
    {
        intent: props.intent,
        type: props.type,
        disabled: props.disabled
    });
});
</script>

<template>
    <div class="field-group">
        <Label :for="props.id" :required="props.required">
            {{ props.label }}      
        </Label>
        <component :class="fieldClass" :is="props.as" :type="props.type" :placeholder="props.placeholder">
            <slot v-bind="props" />
        </component>
    </div>
</template>