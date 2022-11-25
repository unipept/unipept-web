<template>
    <v-card class="d-flex flex-column flex-grow-1">
        <v-tabs
            class="flex-grow-0"
            style="pointer-events: none;"
            slider-color="primary"
            background-color="primary"
            dark
        >
            <v-tab>Metaproteomics Analysis</v-tab>
        </v-tabs>

        <v-card-text v-if="multiAnalysisStore.empty">
            <span>Please add one or more datasets by clicking the plus button above...</span>
        </v-card-text>

        <div v-else class="growing-list">
            <v-list two-line v-model="multiAnalysisStore.activeAssayStatus">
                <v-list-item
                    v-for="assayStatus in assayStatuses"
                    :key="assayStatus.assay.id"
                    :value="assayStatus"
                    @click="activateAssay(assayStatus.assay)"
                    ripple
                >
                    <v-list-item-action>
                        <div v-if="multiAnalysisStore.analysisCompleted(assayStatus.assay.id)" class="select-dataset-radio">
                            <v-radio-group v-model="multiAnalysisStore.activeAssayStatus">
                                <v-radio :value="assayStatus"></v-radio>
                            </v-radio-group>
                        </div>
                        <v-progress-circular v-else 
                            :rotate="-90" 
                            :size="24" 
                            :value="assayStatus.progress.currentValue" 
                            color="primary"
                        />
                    </v-list-item-action>
                    
                    <v-list-item-content>
                        <v-list-item-title>
                            {{ assayStatus.assay.name }}
                        </v-list-item-title>
                        <v-list-item-subtitle v-if="done(assayStatus)">
                            {{ assayStatus.assay.amountOfPeptides }} peptides
                        </v-list-item-subtitle>
                        <v-list-item-subtitle v-else-if="calculating(assayStatus)">
                            Computing estimated time remaining...
                        </v-list-item-subtitle>
                        <v-list-item-subtitle v-else>
                            ~{{ StringUtils.secondsToTimeString(assayStatus.progress.eta) }} remaining...
                        </v-list-item-subtitle>
                    </v-list-item-content>

                    <v-list-item-action>
                        <v-list-item-action-text>
                            {{ dateToString(assayStatus.assay.createdAt) }}
                        </v-list-item-action-text>
                        <tooltip message="Remove assay from analysis.">
                            <v-icon @click="removeAssay(assayStatus.assay)" v-on:click.stop>mdi-delete-outline</v-icon>
                        </tooltip>
                    </v-list-item-action>
                </v-list-item>
            </v-list>
        </div>
    </v-card>
</template>

<script setup lang="ts">
import useMultiAnalysis from '@/stores/MultiAnalysisStore';
import { storeToRefs } from 'pinia';
import { Assay, StringUtils, Tooltip } from 'unipept-web-components';
import { withDefaults, defineProps } from 'vue';

export interface Props {
    assaySelectionInProgress: boolean
}

withDefaults(defineProps<Props>(), {
    assaySelectionInProgress: false
});

const multiAnalysisStore = useMultiAnalysis();

const { assayStatuses } = storeToRefs(multiAnalysisStore);

const done = (assayStatus: any) => {
    //console.log(JSON.stringify(assayStatus));
    return !assayStatus.analysisInProgress;
};

const calculating = (assayStatus: any) => {
    return assayStatus.progress.currentValue === -1;
};

const activateAssay = (assay: Assay) => {
    multiAnalysisStore.activateAssay(assay);
}

const removeAssay = (assay: Assay) => {
    multiAnalysisStore.removeAssay(assay);
};

const dateToString = (date: Date) => {
    date = new Date(date);

    const year = date.getFullYear();
    const month = date.getMonth() + 1;
    const day = date.getDate();

    return `${day}/${month}/${year}`;
};
</script>