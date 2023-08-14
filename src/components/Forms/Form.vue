<script setup>
import { computed, provide, ref } from "vue";
import { v4 as uuid } from "uuid";
import Buttons from './Buttons.vue';
import Button from './Button.vue';

const props = defineProps(
{
    name: String,
    action: String,
    method: String,
});

const errors = ref({});

/**
*   Cette fonction permet d'envoyer le formulaire et de vérifier si tout est bon.
*
*   @param {Array} fields
**/
function submit(fields = []) 
{

}
</script>

<template>
    <form :action="props.action" :method="props.method" class="form" enctype="multipart/form-data">
        <slot />
        <Buttons>
            <Button intent="primary" type="submit">Valider</Button>
            <Button intent="danger" type="reset">Annuler</Button>
        </Buttons>
    </form>
</template>