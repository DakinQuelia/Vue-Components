<script setup>
import { computed, provide } from "vue";
import { v4 as uuid } from "uuid";

const props = defineProps(
{
    name: String,
    required: Boolean
});
</script>

<template>
    <label :for="props.name" class="label">
        <slot />
        <span class="required" v-if="props.required">*</span>
    </label>
</template>