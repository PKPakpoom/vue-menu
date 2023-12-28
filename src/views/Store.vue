<template>
    
    <v-container>
        <v-row>
            <v-col
                v-for="n in foods.length"
                :key="n"
                cols="12"
                sm="2"
            >
                <v-card
                    class="mx-auto"
                    max-width="344"
                >
                    <v-img
                        v-bind:src="(foods[n-1] as any).meals[0].strMealThumb"
                        height="200px"
                        cover
                    ></v-img>

                    <v-divider></v-divider>

                    <v-card-title>
                        {{ (foods[n-1] as any).meals[0].strMeal }}
                    </v-card-title>

                    <v-card-actions>
                        <v-btn
                            color="blue darken-1"   
                            prepend-icon="mdi-help-circle"
                        >
                            show
                            <v-dialog
                                activator="parent"
                                width="auto"
                            >
                                <v-card>
                                    <v-card-title>
                                        {{ (foods[n-1] as any).meals[0].strMeal }}
                                    </v-card-title>
                                    <v-divider></v-divider>
                                    <v-card-text>
                                        <v-list-item v-for="ingredient in getIngredients((foods[n-1] as any).meals[0])">
                                            <v-list-item-content>
                                                <v-list-item-title>{{ ingredient  }}</v-list-item-title>
                                            </v-list-item-content>
                                        </v-list-item>
                                    </v-card-text>
                                </v-card>

                            </v-dialog>
                        </v-btn>
                    </v-card-actions>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script lang="ts" setup>
    import { reactive, onMounted } from 'vue';

    interface Food {
        selected: boolean;
        meals: { strMealThumb: string, strMeal: string }[];
    }

    const foods = reactive<Food[]>([]);

    
    
    const fetchFoods = async () => {
        const response = await fetch('https://www.themealdb.com/api/json/v1/1/random.php');
        const data = await response.json()
        .then(data => data)
        .catch(err => fetchFoods());
        foods.push(data as Food);
        return response;
    };
    
    const getIngredients = (food: any): string[] => {
        const ingredients: string[] = [];
        for (let i = 1; i <= 20; i++) {
            const ingredient = food[`strIngredient${i}`];
            if (ingredient) {
                ingredients.push(ingredient);
            } else {
                break;
            }
        }
        
        return ingredients;
    }

    onMounted(() => {
        let arr: Promise<Response>[] = [];
        for (let i = 0; i < 30; i++) {
            arr.push(fetchFoods());
        }
        Promise.all(arr).then().catch(err => console.log(err));
    });
    
</script>
