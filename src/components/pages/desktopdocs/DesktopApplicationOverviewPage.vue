<template>
    <v-container>
        <h1 class="font-weight-light">
            Application overview
        </h1>
        <h3 class="font-weight-light mb-2">
            This document provides a quick overview and explanation of the main application window and how this is
            composed of smaller components.
        </h3>
        <header-body-card title="Application window" id="application_window" class="mb-5">
            <div class="d-flex justify-center ma-5">
                <v-img :src="require('@/assets/documentation/desktop/application_overview/desktop_application_structure.png')"
                    max-width="800"
                    contain
                    class="screenshot"/>
            </div>
            <p>
                The application window will always consists of two main parts. On the far left (depicted in red in the
                screenshot), you will find the sidebar. The sidebar is always visible and can be used to navigate
                between the different windows of this application (each corresponding to a specific feature or
                functionality). On the right (depicted in purple in the screenshot) the main content view is located.
                This is the part of the application that will change depending on the selected tab in the sidebar.
            </p>
        </header-body-card>

        <header-body-card title="Sidebar" id="sidebar">
            <p>
                Below you will find a short overview of all buttons that are present in the sidebar and what the
                associated functionality of these buttons is. Dedicated documentation pages are available for each of
                the functions / components described below.
            </p>
            <h3>Home</h3>
            <div class="d-flex mb-2">
                <v-img :src="require('@/assets/documentation/desktop/application_overview/desktop_home_button.png')"
                   max-width="50"
                   contain
                   class="mr-2" />
                <div>
                    The homepage of the application is dedicated to project management. Everytime you want to switch
                    between projects, create a new project, or open an existing one, you will have to go back to this
                    page.
                </div>
            </div>

            <h3>Single assay analysis</h3>
            <div class="d-flex mb-2">
                <v-img :src="require('@/assets/documentation/desktop/application_overview/desktop_single_analysis_button.png')"
                   max-width="50"
                   contain
                   class="mr-2" />
                <div>
                    In order to analyse invidual samples (and browse the analysis results), you will have to navigate
                    to the &quot;single assay analysis&quot; page. This page allows you to manage the contents of your
                    project, manage studies and assays and browse the results of the analyses that were performed
                    earlier.
                </div>
            </div>

            <h3>Inter-assay comparative analysis</h3>
            <div class="d-flex mb-2">
                <v-img :src="require('@/assets/documentation/desktop/application_overview/desktop_comparative_button.png')"
                   max-width="50"
                   contain
                   class="mr-2" />
                <div>
                    Unipept Desktop allows you to compare features between distinct samples. By navigating to the
                    &quot;inter-assay comparative analysis&quot; page, you can select multiple samples in the project
                    explorer view on the left and a set of features that should be compared between these samples. After
                    properly selecting and configuring all settings on this page, an interactive heatmap visualization
                    will automatically be generated.
                </div>
            </div>

            <h3>Tryptic peptide analysis</h3>
            <div class="d-flex mb-2">
                <v-img :src="require('@/assets/documentation/desktop/application_overview/desktop_single_peptide_button.png')"
                       max-width="50"
                       contain
                       class="mr-2" />
                <div>
                    All analysis types that have been described above require a project to be loaded. They perform a
                    specific analysis on a set of peptides and aggregate the results. In contrast, the &quot;tryptic
                    peptide analysis&quot; page allows you to perform a specific analysis on a single peptide. This
                    component type generates a report with all information that is known about a single tryptic peptide
                    and produces a list of all proteins that match with this peptide, as well as a taxonomic and
                    functional annotation.
                </div>
            </div>

            <h3>Targeted database management</h3>
            <div class="d-flex mb-2">
                <v-img :src="require('@/assets/documentation/desktop/application_overview/desktop_database_button.png')"
                       max-width="50"
                       contain
                       class="mr-2" />
                <div>
                    If you want to construct, delete or modify a targeted protein reference database (for use with the
                    metaproteomics analysis pipeline), you need to navigate to the
                    &quot;targeted database management&quot; page. This page will provide you with a list of all
                    available databases, their current construction status and a handy wizard that will guide you
                    through the database construction process.
                </div>
            </div>

            <h3>Settings</h3>
            <div class="d-flex">
                <v-img :src="require('@/assets/documentation/desktop/application_overview/desktop_settings_button.png')"
                       max-width="50"
                       contain
                       class="mr-2" />
                <div>
                    The behaviour of the Unipept Desktop application can be finetuned in a lot of cases. All available
                    configuration options can be configured on the &quot;settings&quot; page. Some examples of this are
                    the location of the Unipept Desktop application data directory, configuration settings for
                    communication between Unipept and the local Docker Daemon, etc.
                </div>
            </div>
        </header-body-card>
    </v-container>
</template>

<script setup lang="ts">
import HeaderBodyCard from "@/components/cards/HeaderBodyCard.vue";
</script>
