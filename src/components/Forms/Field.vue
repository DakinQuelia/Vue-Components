<script setup>
import { computed, provide, inject } from "vue";
import { v4 as uuid } from "uuid";
import { cva } from "class-variance-authority";
import Label from './Label.vue';
import HelperMessage from './HelperMessage.vue';
import ErrorMessage from './ErrorMessage.vue';

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
    modelValue: [ String, Number ],
    type: String,
    label: String,
    ariaDescribedBy: String,
    disabled: Boolean,
    required: Boolean,
    invalid: Boolean,
    placeholder: String,
    error: String,
    help: String,
    prepend: Object,
    append: Object,
    radios: Array,
    checkboxes: Array
});

const emit = defineEmits([ "update:modelValue" ]);

const helpID = computed(() => 
{
    return !!props.help ? `help-${props.id}` : null;
});

const errorID = computed(() => 
{
    return !!props.error ? `error-${props.id}` : null;
});

const fieldClass = computed(() => 
{
    return cva("input-control", 
    {
        variants: 
        {
            invalid: "error",
            disabled: 
            {
                true: "disabled",
            }
        }
    })(
    {
        invalid: props.error,
        type: props.type,
        disabled: props.disabled
    });
});

provide("field", computed(() => 
  {
    return {
        ...props,
        invalid: !!props.error,
        ariaDescribedBy: helpID.value,
    };
  })
);

const field = inject("field", props);

</script>

<template>
    <div class="field-group">
        <div class="col">
            <Label :for="field.id" :required="field.required" v-if="field.label">
                {{ field.label }}      
            </Label>
        </div>
        <div class="col">
            <component :class="[fieldClass, field.invalid ? 'error' : '']" :is="field.as" :id="field.id" :type="field.type" :placeholder="field.placeholder" :value="field.modelValue" @input="$event => emit('update:modelValue', $event.target.value)" :required="field.required" aria-describedby="helpID">
                <slot v-bind="field" />
            </component>
            <Label :for="field.id" :required="field.required" v-if="field.radio">
                {{ field.label }}      
            </Label>
            <ErrorMessage v-if="field.error" :id="errorID">
                {{ field.error }}
            </ErrorMessage>
            <HelperMessage v-if="field.help" :id="helpID">
                {{ field.help }}
            </HelperMessage>  
        </div>
    </div>
</template>