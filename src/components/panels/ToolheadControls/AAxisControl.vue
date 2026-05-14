<template>
    <v-row dense class="mt-2">
        <v-col class="text-center">
            <v-item-group class="_btn-group row no-gutters">
                <v-btn
                    v-for="steps of stepsAsorted"
                    :key="'a-' + steps"
                    :disabled="['printing'].includes(printer_state)"
                    class="btnMinWidthAuto col btnGroup"
                    @click="doSendMoveA(steps * -1)">
                    <span class="body-2">-{{ steps }}</span>
                </v-btn>
                <v-btn color="primary" class="font-weight-bold btnHomeAxis btnGroup">A</v-btn>
                <v-btn
                    v-for="steps of stepsAsortedReverse"
                    :key="'a+' + steps"
                    :disabled="['printing'].includes(printer_state)"
                    class="btnMinWidthAuto col btnGroup"
                    @click="doSendMoveA(steps)">
                    <span class="body-2">+{{ steps }}</span>
                </v-btn>
            </v-item-group>
        </v-col>
    </v-row>
</template>

<script lang="ts">
import { Component, Mixins } from 'vue-property-decorator'
import BaseMixin from '@/components/mixins/base'
import ControlMixin from '@/components/mixins/control'

@Component
export default class AAxisControl extends Mixins(BaseMixin, ControlMixin) {
    get stepsAsorted() {
        return [...(this.$store.state.gui.control.stepsA ?? [])].sort(function (a, b) {
            return b - a
        })
    }

    get stepsAsortedReverse() {
        return [...(this.$store.state.gui.control.stepsA ?? [])].sort(function (a, b) {
            return a - b
        })
    }
}
</script>

<style scoped>
.btnHomeAxis {
    width: 36px;
    min-width: 36px !important;
}

.btnGroup {
    height: 28px !important;
}

.btnMinWidthAuto {
    min-width: auto !important;
}

._btn-group {
    border-radius: 4px;
    display: inline-flex;
    flex-wrap: nowrap;
    max-width: 100%;
    min-width: 100%;
    width: 100%;

    .v-btn {
        border-radius: 0;
        border-color: rgba(255, 255, 255, 0.12);
        border-style: solid;
        border-width: thin;
        box-shadow: none;
        height: 28px;
        opacity: 0.8;
        min-width: auto !important;
    }

    .v-btn:first-child {
        border-top-left-radius: inherit;
        border-bottom-left-radius: inherit;
    }

    .v-btn:last-child {
        border-top-right-radius: inherit;
        border-bottom-right-radius: inherit;
    }

    .v-btn:not(:first-child) {
        border-left-width: 0;
    }
}

html.theme--light ._btn-group .v-btn {
    border-color: rgba(0, 0, 0, 0.12);
}
</style>
