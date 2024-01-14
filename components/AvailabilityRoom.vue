<template>
    <v-sheet class="bg-transparent av-card">
        <div>
            <div class="pa-4">
                <div :class="`d-flex align-center ${mealPlanClasses[props.offer.meal_plan_code].color}`">
                    <v-icon size="x-small" :icon="mealPlanClasses[props.offer.meal_plan_code].icon"></v-icon>
                    <p class="pl-2">{{ mealPlanClasses[props.offer.meal_plan_code].text }}</p>
                </div>
                <div :class="`d-flex align-center ${cancelPolicyClasses[props.offer.cancel_policy_code].color}`">
                    <v-icon size="x-small" :icon="cancelPolicyClasses[props.offer.cancel_policy_code].icon"></v-icon>
                    <p class="pl-2">{{ props.offer.cancel_policy_description }}</p>
                </div>
            </div>

            <div class="d-flex flex-row align-end pa-4">
                <div class="mr-auto">
                    <v-btn variant="text" size="small" class="text-none bg-red rounded-0 font-weight-medium text-uppercase">
                        Save {{ getDiscount(props.offer.pricing_data.rate_nightly,
                            props.offer.pricing_data.strikethrough_rate_nightly) }}% Today
                    </v-btn>

                    <p class="text-caption text-decoration-line-through text-grey-lighten-1"
                        v-if="props.offer.pricing_data.strikethrough_rate_nightly > 0">
                        {{ formatIDR(props.offer.pricing_data.strikethrough_rate_nightly) }}
                    </p>
                    <p>
                        <span class="text-h6">{{ formatIDR(props.offer.pricing_data.rate_nightly) }}</span> / night &midast;
                    </p>
                    <p>
                        Total &middot; {{ formatIDR(props.offer.pricing_data.net_rate_nightly_with_bonus) }}
                    </p>
                    <p class="text-caption">After tax & fees</p>
                    <p class="text-caption">* Member-only price, valid in app only</p>
                </div>
                <div class="d-flex flex-column">
                    <v-btn class="text-none font-bold" color="#007aff">Book Now</v-btn>
                    <div class="d-flex items-center py-2">
                        <v-icon color="blue" size="x-small" icon="mdi-star"></v-icon>
                        <p class="text-blue text-caption">Collect 3 Points</p>
                    </div>
                </div>

            </div>
        </div>
    </v-sheet>
</template>

<script setup>
const props = defineProps({
    offer: {
        type: Object,
        default: {}
    },
    lastItem: {
        type: Boolean,
        default: false
    }
})

function getDiscount(afterDiscount, total) {
    return Math.floor(afterDiscount / total * 100)
}

function formatIDR(amount) {
    const IDR = new Intl.NumberFormat('id-ID', {
        style: 'currency',
        currency: 'IDR'
    })

    return IDR.format(amount)
}

const cancelPolicyClasses = {
    'NR': {
        icon: 'mdi-credit-card-off-outline',
        color: 'text-red'
    },
    'FC': {
        icon: 'mdi-credit-card-check',
        color: 'text-green'
    }
}

const mealPlanClasses = {
    'BB': {
        icon: 'mdi-silverware-fork-knife',
        text: 'Free Breakfast',
        color: 'text-green'
    },
    'RO': {
        icon: 'mdi-cup-off',
        text: 'Without Breakfast'
    }
}

</script>

<style>
.av-card {
    border-top: 1px solid #ebe9e9 !important;
}
</style>