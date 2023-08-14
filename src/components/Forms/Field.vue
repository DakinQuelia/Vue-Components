<script setup>
import { computed, provide } from "vue";
import { v4 as uuid } from "uuid";
import Label from 'Label.vue';

const props = defineProps(
{
    id: 
    {
        type: String,
        default: () => `field-${uuid()}`,
    },

    label: String,
    required: Boolean,
    error: String,
    help: String,
});

const ariaDescribedBy = computed(() => 
{
    return !!props.help ? `help-${uuid()}` : null;
});
</script>

<template>
    <div>
        <Label></Label>
        <slot v-bind="props" />
    </div>
</template>