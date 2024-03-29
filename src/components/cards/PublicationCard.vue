<template>
    <v-card>
        <v-card-title class="blue white--text">
            {{ title }}
        </v-card-title>
        <v-card-subtitle class="blue white--text">
            {{ authors.length == 1 ? authors[0] : authors.slice(0, -1).join(", ") + ', and ' + authors[authors.length - 1] }}
        </v-card-subtitle>

        <v-divider />

        <v-card-text>
            <v-row>
                <v-col cols=12 md=8 xl=9>
                    <h2 class="mb-3">Abstract</h2>
                    <slot name="abstract"></slot>

                    <h2 class="mt-5 mb-3">Citation</h2>
                    {{ authors.length == 1 ? authors[0] : authors.slice(0, -1).join(", ") + ', and ' + authors[authors.length - 1] }}
                    <br><b>{{ title }}</b>
                    <br>{{ journal + ", " + year + (extra ? ", " + extra : extra) }}
                    <br>
                    <div class="d-flex">
                        <v-icon small>
                            mdi-link-variant
                        </v-icon>
                        <RLink :to="'https://' + doi">{{ doi }}</RLink>

                        <v-icon class="ps-2" small>
                            mdi-link-variant
                        </v-icon>
                        <RLink :to="googleScholar">Google Scholar</RLink>
                    </div>
                </v-col>
                <v-col cols=12 md=4 xl=3>
                    <RLink :to="'https://' + doi">
                        <v-hover>
                            <template v-slot:default="{ hover }">
                                <v-card :elevation="hover ? 6 : 2">
                                    <v-img :src="image" :alt="image" />
                                </v-card>
                            </template>
                        </v-hover>
                    </RLink>
                </v-col>
            </v-row>
        </v-card-text>
    </v-card>
</template>

<script setup lang="ts">
import { defineProps, withDefaults } from 'vue';
import RLink from '../highlights/ResourceLink.vue';

export interface Props {
    title: string,
    authors: string[],
    journal: string,
    year: string,
    extra?: string,
    doi: string,
    googleScholar: string,
    image: String
}

withDefaults(defineProps<Props>(), {
    extra: ""
});
</script>
