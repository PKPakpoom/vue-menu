<template>
    <v-container
        class="fill-width ma-5 pa-5"
        fluid
    >
        <v-row
            align="center"
            justify="center"
        >
            <v-card
                class="d-flex justify-center align-center"
                max-width="500"
            >
                <v-card-title>
                    Theme
                </v-card-title>
                <v-btn
                    v-if="theme.global.current.value.dark"
                    prepend-icon="mdi-lightbulb"
                    variant="outlined"
                    @click="toggleTheme"
                >
                    Dark
                </v-btn
                ><v-btn
                    v-else
                    prepend-icon="mdi-lightbulb"
                    variant="outlined"
                    @click="toggleTheme"
                >
                    Light
                </v-btn>

            </v-card>

        </v-row>
    </v-container>
</template>

<script lang="ts" setup>
    import { useTheme } from 'vuetify/lib/framework.mjs';
    
    const theme = useTheme();

    function toggleTheme() {
        theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
    }
</script>