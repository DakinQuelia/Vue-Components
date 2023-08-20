<script setup>
import { ref, computed, watch } from "vue";
import { CheckIcon } from "@heroicons/vue/20/solid";
import Label from './Label.vue';
import HelperMessage from './HelperMessage.vue';
import ErrorMessage from './ErrorMessage.vue';
import SelectorIcon from "../Icons/SelectorIcon.vue";

const props = defineProps({
    label: String,
    default: String,
    options: 
    {
        type: Array,
        default: () => [],
    },
    modelValue: [String, Number, Array],
    placeholder: 
    {
        type: String,
        default: "Sélectionnez une option",
    },
    multiple: Boolean,
    error: String
});

const emit = defineEmits(["update:modelValue"]);
const label = computed(() => 
{
    return props.options.filter(option => 
    {
        if (Array.isArray(props.modelValue)) 
        {
            return props.modelValue.includes(option.value);
        }

        return props.modelValue === option.value;

    }).map(option => option.label).join(", ");
});
</script>

<template>
    <div class="field-group">
        <div class="col">
            <Label :for="props.id" :required="props.required" v-if="props.label">
                {{ props.label }}      
            </Label>
        </div>
        <div class="col">
            <div class="selector-box" :model-value="props.modelValue" @update:modelValue="value => emit('update:modelValue', value)" tabindex="0">
                <div class="selector-select">
                    <div class="selector-input">
                        <span class="block truncate" v-if="label">{{ label }}</span>
                        <span class="placeholder" v-else="props.placeholder">{{ props.placeholder }}</span>
                    </div>
                    <span class="selector">
                        <SelectorIcon aria-hidden="true" class="selector-icon" />
                    </span>
                </div>
                <transition leave-active-class="transition duration-100 ease-in" leave-from-class="opacity-100" leave-to-class="opacity-0">
                <div class="selector-box-options">
                    <ul>
                        <li :class="[active ? 'item active' : 'item', ]" v-for="option in props.options" :key="option.label" :value="option.value" as="template">
                            <span :class="[selected ? 'font-medium' : 'font-normal', 'block truncate' ]">{{ option.label }}</span>
                            <span v-if="selected" class="item-icon">
                                <CheckIcon aria-hidden="true" class="w-5 h-5" />
                            </span>
                        </li>
                    </ul>
                </div>    
                </transition>
            </div>
            <ErrorMessage v-if="props.error">
                {{ props.error }}
            </ErrorMessage>
        </div>
    </div>
</template>