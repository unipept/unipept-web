<template>
    <v-card>
        <v-tabs
            style="pointer-events: none;"
            slider-color="primary"
            background-color="primary"
            dark
        >
            <v-tab>Search for a single tryptic peptide</v-tab>
        </v-tabs>

        <v-card-text>
            <router-link
                :to="{
                    name: 'tpaResult',
                    params: { sequence: sequence },
                    query: { equate: equate_il }
                }"
                v-slot="{ navigate }"
            >
                <v-form v-model="validForm" @submit="navigate">
                    <v-row>
                        <v-col class="pb-0" cols=12>
                            <v-text-field
                                class="pt-0 mt-0"
                                v-model.trim="sequence"
                                label="Sequence"
                                :rules="sequenceRules"
                            ></v-text-field>
                        </v-col>
                    </v-row>

                    <v-row>
                        <v-col class="py-0" cols=12 md=6>
                            <v-switch
                                v-model="equate_il"
                                label="Equate I and L?"
                                inset
                            ></v-switch>
                        </v-col>

                        <v-col class="d-flex" cols=12 md=6>
                            <v-spacer />
                            <v-btn
                                color="primary"
                                :disabled="!validForm"
                                type="submit"
                            >
                                <v-icon class="pe-1">mdi-magnify</v-icon> Search
                            </v-btn>
                        </v-col>
                    </v-row>
                </v-form>
            </router-link>
        </v-card-text>
    </v-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const validForm = ref(false);
const sequence = ref("");
const equate_il = ref(true);

const sequenceRules = [
    (value: string) => /^[A-Z]+$/.test(value.toUpperCase()) || "Peptide can only consist of letters",
    (value: string) => value.length >= 5 && value.length <= 50 || "Peptide should consist of 5 to 50 characters"
];
</script>