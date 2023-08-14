<script setup>
import { ref } from "vue";
import { EnvelopeIcon } from "@heroicons/vue/20/solid";
import Tooltip from './components/Tooltip.vue';
import Alert from './components/Alert.vue';
import Form from './components/Forms/Form.vue';
import Field from './components/Forms/Field.vue';

const showAlert = ref(true);
</script>

<template>
    <div class="w-[700px]">
        <Form action="/" method="POST" name="test">
            <Field as="input" type="text" id="name" label="Nom d'utilisateur" placeholder="Nom d'utilisateur" error="Nom d'utilisateur invalide." />
            <Field as="textarea" id="message" label="Message" placeholder="Message" required error="Le message est obligatoire." help="Mon aide"  />
        </Form>
    </div>
    <!--
    <div class="grid min-h-screen place-content-center gap-4">   
        <Alert title="Titre" intent="info" onDismiss="true" :show="showAlert" :on-dismiss="() => showAlert = false">
            Mon message d'information.
        </Alert>

        <div class="flex gap-5 flex-wrap">
            <Button intent="primary" :leftIcon="EnvelopeIcon" as="a" href="#">Mon lien</Button>
            <Button intent="secondary" :leftIcon="EnvelopeIcon" as="a" href="#">Mon lien 2</Button>
            <Button intent="tertiary" :leftIcon="EnvelopeIcon" as="a" href="#">Mon lien 3</Button>
        </div>

        <div class="flex gap-5 flex-wrap">
            <Button intent="primary" :leftIcon="EnvelopeIcon">Mon bouton</Button>
            <Button intent="success" :leftIcon="EnvelopeIcon">Valider</Button>
            <Button intent="danger" :leftIcon="EnvelopeIcon">Annuler</Button>
            <Button intent="tertiary" :leftIcon="EnvelopeIcon">Mon lien 3</Button>
        </div>

        <div class="flex gap-5 flex-wrap">
            <Button intent="primary" :leftIcon="EnvelopeIcon" loading>Mon bouton</Button>
            <Button intent="secondary" :leftIcon="EnvelopeIcon" loading>Mon bouton</Button>
            <Button intent="tertiary" :leftIcon="EnvelopeIcon" loading>Annuler</Button>
            <Button intent="success" :leftIcon="EnvelopeIcon" loading>Valider</Button>
            <Button intent="danger" :leftIcon="EnvelopeIcon" loading>Annuler</Button>
        </div>

        <div class="flex gap-5 flex-wrap">
            <Button intent="primary" :leftIcon="EnvelopeIcon" disabled>Mon bouton</Button>
            <Button intent="success" :leftIcon="EnvelopeIcon" disabled>Valider</Button>
            <Button intent="danger" :leftIcon="EnvelopeIcon" disabled>Annuler</Button>
        </div>
        
        <Alert title="Titre" intent="success" onDismiss="true" :show="showAlert" :on-dismiss="() => showAlert = false">
            Mon message d'information.
        </Alert>

        <Alert title="Titre" intent="danger" onDismiss="true" :show="showAlert" :on-dismiss="() => showAlert = false">
            Mon message d'information.
        </Alert>

        <Alert title="Titre" intent="warning" onDismiss="true" :show="showAlert" :on-dismiss="() => showAlert = false">
            Mon message d'information.
        </Alert>

        <Tooltip content="Ceci est mon infobulle en haut d'un long texte..." placement="top">
            <button class="tooltip-button">Cliquez ici</button>
        </Tooltip>

        <Tooltip content="Ceci est mon infobulle en bas d'un long texte..." placement="bottom">
            <button class="tooltip-button green">Cliquez ici</button>
        </Tooltip>

        <Tooltip content="Ceci est mon infobulle à gauche d'un long texte..." placement="left">
            <button class="tooltip-button red">Cliquez ici</button>
        </Tooltip>

        <Tooltip content="Ceci est mon infobulle à droite d'un long texte..." placement="right">
            <button class="tooltip-button orange">Cliquez ici</button>
        </Tooltip>
    </div>
    -->
</template>