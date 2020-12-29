<template>
    <div>
        <form-wizard class="form" title="Hospital Profile" subtitle="Please complete this form..." color="#008cff" stepSize="sm">
            <tab-content title="Summary" :beforeChange="sendSummary">
                <v-row>
                    <v-col>
                        <v-text-field v-model="summary.street_addr" label="Street Address"></v-text-field>
                        <v-select v-model="summary.state" :items="states" label="State"></v-select>
                        <v-text-field v-model="summary.hospital_name" label="Hospital Name"></v-text-field>
                    </v-col>
                    <v-col>
                        <v-text-field v-model="summary.city" label="City"></v-text-field>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col>
                        <v-text-field v-model="summary.profile_name" label="Name for Hospital Profile"></v-text-field>
                        <v-text-field v-model="summary.year_founded" label="Year Founded"></v-text-field>
                    </v-col>
                    <v-col>
                        <v-text-field v-model="summary.profile_year" label="Year for Hospital Profile">
                            <template v-slot:prepend>
                                <v-tooltip bottom>
                                <template v-slot:activator="{ on }">
                                    <v-icon v-on="on">mdi-help-circle-outline</v-icon>
                                </template>
                                For comparing data across years, likely an accounting year, e.g. September to September
                                </v-tooltip>
                            </template>
                        </v-text-field>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col>
                        <v-select v-model="summary.part_of_HCO" :items="yn" label="Is your hospital part of a larger health care organization?"></v-select>
                        <v-select v-model="summary.other_healthcare_entities" :items="yn" label="Does hispital food staff provide prepared food to other health care entities?"></v-select>
                        <v-select v-model="summary.hospital_incorporated" :items="incorporated" label="How is the hospital incorporated?"></v-select>
                    </v-col>
                    <v-col>
                        <v-text-field v-if="summary.part_of_HCO" v-model="summary.HCO_name" label="HCO Name"></v-text-field>
                        <v-text-field v-if="summary.other_healthcare_entities" v-model="summary.name_other_entities" label="Please name these..."></v-text-field>
                    </v-col>
                </v-row>
                <v-text-field v-model="summary.member_of_associations" label="Please list any local, regional, state, or national associations of which your organization is a dues paying member."></v-text-field>
                <v-row>
                    <v-col>
                        <v-select v-model="summary.mission_statement_yn" :items="yn" label="Does your hospital food system have a mission statement?"></v-select>
                        <v-textarea v-if="summary.mission_statement_yn" label="Please provide your mission statement." v-model="summary.mission_statement"></v-textarea>
                    </v-col>
                    <v-col>
                        <v-select v-if="summary.mission_statement_yn" multiple v-model="summary.mission_statement_loc" :items="locations" label="Where is the mission statement located? (Select all that apply)"></v-select>
                        <v-text-field v-if="summary.mission_statement_yn" label="When was the mission statement written or last updated?" v-model="summary.mission_last_updated"></v-text-field>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col>
                        <v-select v-model="summary.food_procurement_policy" label="Who makes decisions on hospital food procurement policy?"></v-select>
                        <v-select v-model="summary.food_system_staff" label="Who makes decisions on hospital food system staffing?"></v-select>
                        <v-file-input label="Upload Logo Here"></v-file-input>
                    </v-col>
                    <v-col>
                        <v-select v-model="summary.food_menus" label="Who makes decisions on hospital food menus?"></v-select>
                        <v-select v-model="summary.info_requests" label="Who responds to information requests from patients, staff, or visitors?"></v-select>
                    </v-col>
                </v-row>                
            </tab-content>
            <tab-content title="Management">
                <HospitalManagement />
            </tab-content>
            <tab-content title="Vendors">
                <HospitalVendors />
            </tab-content>
            <tab-content title="Community">
                <HospitalCommunity />
            </tab-content>
        </form-wizard>
        <v-select :items="states"></v-select>
    </div>
</template>
<script>
// /Users/rachelfu/Desktop/f2f-hospital-frontend/src/components/HospitalVendors.vue
import {mapActions} from 'vuex';
import HospitalManagement from '@/components/HospitalManagement.vue';
import HospitalVendors from '@/components/HospitalVendors.vue';
import HospitalCommunity from '@/components/HospitalCommunity.vue';
export default {
    components: {
        HospitalManagement,
        HospitalVendors,
        HospitalCommunity
    },
    data(){
        const summary = {
            street_addr: "",
            city: "",
            state: "",
            hospital_name: "",
            profile_year: "",
            profile_name: "",
            year_founded: "",
            part_of_HCO: null,
            HCO_name: "",
            other_healthcare_entities: null,
            name_other_entities: "",
            hospital_incorporated: "",
            member_of_associations: "",
            mission_statement_yn: null,
            mission_statement_loc: "",
            mission_statement: "",
            mission_last_updated: "",
            food_procurement_policy: "",
            food_menus: "",
            food_system_staff: "",
            info_requests: "",
            logo_name: "",
            logo_content_type: "",
            logo_data: ""
        }
        const states = ['Alabama','Alaska', 'Arizona', 'Arkansas','California','Colorado','Connecticut','Delaware','Florida','Georgia','Hawaii','Idaho','Illinois','Indiana','Iowa','Kansas','Kentucky','Louisiana','Maine','Maryland','Massachusetts','Michigan','Minnesota','Mississippi','Missouri','Montana','Nebraska','Nevada','New Hampshire','New Jersey','New Mexico','New York','North Carolina','North Dakota','Ohio','Oklahoma','Oregon','Pennsylvania','Rhode Island','South Carolina','South Dakota','Tennessee','Texas','Utah','Vermont','Virginia','Washington','West Virginia','Wisconsin','Wyoming']
        const yn = [{text:"Yes", value: true},{text:"No",value: false}]
        // TODO how do I have them "explain" if they select the option "Other"
        const incorporated = ["Government","LLC","Non-profit","For profit","Partnership","Sole Propriertorship","Other"]
        const locations = ["Website","Manual","Market promotional materials","None of the above","Other"]
        return {
            summary,
            states,
            yn,
            incorporated,
            locations
        }
    },
    methods: {
        ...mapActions(['newSummary']),
        sendSummary(){
            this.newSummary(this.$http, this.summary)
            // console.log(this.summary)
            return true
        }
    }
}
</script>
<style scoped>
.form {
    margin: 9%;
}
</style>