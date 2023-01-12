<template>
    <HeaderBodyCard title="Latest versions">
        <template>
            <v-navigation-drawer
                class="my-n4"
                width="100%"
                permanent
            >
                <v-list>
                    <v-list-item class="px-0 px-sm-5" v-for="item in services" :key="item.name" :to="item.to" link>
                        <v-list-item-icon>
                            <v-icon>{{ item.icon }}</v-icon>
                        </v-list-item-icon>

                        <v-list-item-content v-if="$vuetify.breakpoint.smAndUp" class="fixed-flex-size">
                            <v-list-item-title>{{ item.name }}</v-list-item-title>
                        </v-list-item-content>

                        <v-spacer />

                        <v-chip v-if="item.version"
                            class="ma-2 mb-0 justify-left"
                            small
                            label
                            color="primary"
                        >
                            {{ item.version }}
                        </v-chip>

                        <v-chip v-if="recentDate(item.date, 120)"
                            class="recent-release my-2 mb-0 px-2 justify-left"
                            small
                            label
                            color="green"
                        >
                            <v-icon class="white--text me-2">
                                mdi-flag
                            </v-icon>
                            <span>
                                {{ formatDate(item.date) }}
                            </span>
                        </v-chip>

                        <v-chip v-else-if="item.version"
                            class="my-2 mb-0 px-2 justify-left"
                            small
                            label
                        >
                            <span>
                                {{ formatDate(item.date) }}
                            </span>
                        </v-chip>

                        <v-spacer />

                        <v-list-item-icon>
                            <v-icon>mdi-chevron-right</v-icon>
                        </v-list-item-icon>
                    </v-list-item>
                </v-list>
            </v-navigation-drawer>
        </template>
    </HeaderBodyCard>
</template>

<script setup lang="ts">
import { defineProps } from "vue";
import HeaderBodyCard from "./HeaderBodyCard.vue";

export type Service = {
    name: string,
    icon: string,
    version: string,
    date: string,
    to: string
}

export interface Props {
    services: Service[]
}

const { services } = defineProps<Props>();

const formatDate = (dateString: string) => {
    const date = new Date(dateString);
    return `${date.getDate()}-${date.getMonth() + 1}-${date.getFullYear()}`;
}

const recentDate = (dateString: string, maxDays: number) => {
    const date = new Date(dateString);
    console.log(Math.round((Date.now() - date.getTime()) / (1000 * 60 * 60 * 24)))
    return Math.round((Date.now() - date.getTime()) / (1000 * 60 * 60 * 24)) < maxDays;
}
</script>

<style scoped>
.fixed-flex-size {
    flex: 0 0 100px;
}

.recent-release span {
    display: none !important;
    transition: background 1s;
    color: white;
}

.recent-release:hover span {
    display: contents !important;
    color: white !important;
}

.recent-release:after {
    content: "New release" !important;
    color: white;
}

.recent-release:hover:after {
    content: none !important;
}
</style>