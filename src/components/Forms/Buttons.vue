<script setup>
import { computed, provide, ref } from "vue";
import { v4 as uuid } from "uuid";
</script>

<template>
    <div class="buttons">
        <slot />
    </div>
</template>