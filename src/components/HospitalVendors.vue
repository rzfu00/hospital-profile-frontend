<template>
    <div>
        <v-row>
            <v-col>
                <v-text-field dense label="How many local food vendors did you use during the previous year?"></v-text-field>
            </v-col>
        </v-row>
        
        <v-row>
            <v-col>
                <p> If your food procurment spending is not tax exempt, please list your sales tax rate.</p>
                <v-text-field dense label="State Amount"></v-text-field>
                <v-text-field dense label="County Amount"></v-text-field>
                <v-text-field dense label="Municipality Amount"></v-text-field>
            </v-col>
        </v-row>
        <p>Identify whether the following product categories are exempt from sales tax.  Complete all that apply. </p>
        <v-data-table :headers="headers" :items="categories" hide-default-footer>
            
            <template v-slot:[`item.exempt`]="{ item }">
                <v-simple-checkbox v-model="item.exempt">
                </v-simple-checkbox>
            </template>
        </v-data-table>
        <v-checkbox v-for="item in ServiceItems" v-bind:key="item" :value="item" :label="item" v-model="selectedServices" dense>
        </v-checkbox>
        {{selectedServices}}
    </div>
</template>

<script>
export default {
    data(){
        const ServiceItems = ["Youth-specific activities","Live music","Demonstrations (cooking or planting)","Skills workshops (physical or craft)","Community group meetings for excercise or other"]
        const headers = [
            {
                text: "Cateogry",
                value: "category"
            },
            {
                text: "Exempt",
                value: "exempt"
            },
        ]
        // const categories = ["Produce","Meat & Seafood","Dairy","Eggs","Plants & Flowers","Value-added","Prepared food","Craft/art/services"];
        const categories = [
            {
                category: "Produce",
                exempt: false,
            },
            {
                category: "Meat & Seafood",
                exempt: false,
            },
            {
                category: "Dairy",
                exempt: false,
            },
            {
                category: "Eggs",
                exempt: false,
            },
            {
                category: "Plants & Flowers",
                exempt: false,
            },
            {
                category: "Value-added",
                exempt: false,
            },
            {
                category: "Prepared Food",
                exempt: false,
            },
            {
                category: "Craft/art/services",
                exempt: false,
            },
        ]
        return {
            headers,
            categories,
            ServiceItems,
            selectedServices: []
        }
    }
}
</script>
<style scoped>

</style>