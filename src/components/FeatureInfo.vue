<template lang="pug">
#FeatureInfo.b--black.ba.pv2.ph3.bg-white.ma2(v-show="feature")
    h3.f4.ml4-l {{ p.NAME || '(Unnamed item)' }}
    p.f4.ml4-l {{ p[theme] + selectedLegend.unit}}
</template>

<script>
import { EventBus } from './EventBus';
export default {
    name: "FeatureInfo",
    data: () => ({
        feature: undefined,
        theme: "P_DEN",
    }),
    props: {
        selectedLegend: Object
    },
    computed: {
        p() {
            return this.feature && this.feature.properties || {};
        },
    },
    created() {
        EventBus.$on('feature-clicked', feature => {
            EventBus.$emit('select-feature', feature);
            this.feature = feature;
        });

        EventBus.$on('change-theme', theme => {
                this.theme = theme.type;
        });
    }
}
</script>

<style scoped>
#FeatureInfo th {
    text-align:  right;
}
</style>