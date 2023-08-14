<script setup>
import { ref } from 'vue';
import { computePosition, offset, flip, shift, arrow } from "@floating-ui/dom";

const props = defineProps({
    content: String,
    placement: {
        type: String,
        default: "bottom",
    },
});

const referenceRef = ref();
const tooltipContentRef = ref();
const arrowRef = ref();
const isHidden = ref(true);

/**
*   Cette fonction permet de calculer la position de l'élément.
**/
async function calculatePosition()
{
    const { x, y, middlewareData, placement } = await computePosition(referenceRef.value, tooltipContentRef.value, 
    {
        placement: props.placement,
        middleware: [ offset(8), flip(), shift({ padding: 5 }), arrow({ element: arrowRef.value }) ]
    });

    Object.assign(tooltipContentRef.value.style, 
    {
        left: `${x}px`,
        top:  `${y}px`,
    });

    const { x: arrowX, y: arrowY } = middlewareData.arrow;
    const opposedSide = 
    {
        left: "right",
        right: "left",
        bottom: "top",
        top: "bottom"
    }[placement.split("-")[0]];

    Object.assign(arrowRef.value.style, 
    {
        left: arrowX ? `${arrowX}px` : "",
        top:  arrowY ? `${arrowY}px` : "",
        bottom: "",
        right: "",
        [opposedSide]: "-4px"
    });
}

/**
*   Cette fonction permet d'afficher l'élément.
**/
function show()
{
    isHidden.value = false;

    calculatePosition();
}

/**
*   Cette fonction permet de masquer l'élément.
**/
function hide()
{
    isHidden.value = true;
}
</script>

<template>
    <div class="inline-block">
        <div ref="referenceRef" class="inline-block" @blur="hide" @focus="show" @mouseenter="show" @mouseleave="hide">
            <slot />
        </div>
        <div :class="['tooltip-content', isHidden && 'hidden']" ref="tooltipContentRef" role="tooltip">
            {{ props.content }}
            <div class="tooltip-arrow" ref="arrowRef"></div>
        </div>
    </div>
</template>