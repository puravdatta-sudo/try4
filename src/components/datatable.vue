<template>
    <v-data-table :headers="headers" :items="Teams" sort-by="AutonScore" class="elevation-1">
        <template v-slot:top>
            <v-toolbar flat color="white">
                <v-toolbar-title>My CRUD</v-toolbar-title>
                <v-divider class="mx-4" inset vertical></v-divider>
                <v-spacer></v-spacer>
                <v-dialog v-model="dialog" max-width="500px">
                    <template v-slot:activator="{ on, attrs }">
                        <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">New Item</v-btn>
                    </template>
                    <v-card>
                        <v-card-title>
                            <span class="headline">{{ formTitle }}</span>
                        </v-card-title>

                        <v-card-text>
                            <v-container>
                                <v-row>
                                    <v-col cols="12" sm="6" md="4">
                                        <v-text-field v-model="editedItem.TeamNumber" label="Team Name"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" sm="6" md="4">
                                        <v-text-field v-model="editedItem.AutonPoints" label="Auton Score"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" sm="6" md="4">
                                        <v-text-field v-model="editedItem.TeleScore" label="Tele Score"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" sm="6" md="4">
                                        <v-text-field v-model="editedItem.TotalScore" label="Total Score"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" sm="6" md="4">
                                        <v-text-field v-model="editedItem.MatchNumber" label="Match Number"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" sm="6" md="4">
                                        <v-switch
                                        v-model="Switch1"
                                        :label="'Win?'">

                                        </v-switch>
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-card-text>

                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
                            <v-btn color="blue darken-1" text @click="save">Save</v-btn>
                        </v-card-actions>
                    </v-card>
                </v-dialog>
            </v-toolbar>
        </template>
        <template v-slot:item.actions="{ item }">
            <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
            <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
        </template>
        <template v-slot:no-data>
            <v-btn color="primary" @click="initialize">Reset</v-btn>
        </template>
    </v-data-table>
</template>
<script>
    export default {
        data: () => ({
            dialog: false,
            headers: [
                {
                    text: "Team Name",
                    align: "start",
                    sortable: false,
                    value: "name"
                },
                { text: "Team Number", value: "TeamNumber" },
                { text: "Auton Score", value: "AutonScore" },
                { text: "Tele Op Score", value: "TeleScore" },
                { text: "Total Score", value: "TotalScore" },
                { text: "W/L",value: "Record"},
                { text: "Actions", value: "actions", sortable: false }
            ],
            Teams: [],
            editedIndex: -1,
            editedItem: {
                TeamNumber: "",
                AutonPoints: 0,
                TeleScore: 0,
                TotalScore: 0,
                MatchNumber: 0,
                Record: 0
            },
            defaultItem: {
                TeamNumber: "",
                AutonScore: 0,
                TeleScore: 0,
                TotalScore: 0,
                Record: 0
            }
        }),

        computed: {
            formTitle() {
                return this.editedIndex === -1 ? "New Item" : "Edit Item";
            }
        },

        watch: {
            dialog(val) {
                val || this.close();
            }
        },

        created() {
            this.initialize();
        },

        methods: {
            initialize() {
                this.Teams = [
                    {
                        name: "Frozen Yogurt",
                        TeamNumber: "14614",
                        AutonScore: 159,
                        TeleScore: 6.0,
                        TotalScore: 24,
                        Record: 4.0
                    },
                    {
                        name: "Ice cream sandwich",
                        TeamNumber: "14614",
                        AutonScore: 237,
                        TeleScore: 9.0,
                        TotalScore: 37,
                        Record: 4.3
                    },
                    {
                        name: "Eclair",
                        TeamNumber: "14614",
                        AutonScore: 262,
                        TeleScore: 16.0,
                        TotalScore: 23,
                        Record: 6.0
                    },
                    {
                        name: "Cupcake",
                        TeamNumber: "14614",
                        AutonScore: 305,
                        TeleScore: 3.7,
                        TotalScore: 67,
                        Record: 4.3
                    },
                    {
                        name: "Gingerbread",
                        TeamNumber: "14614",
                        AutonScore: 356,
                        TeleScore: 16.0,
                        TotalScore: 49,
                        Record: 3.9
                    },
                    {
                        name: "Jelly bean",
                        TeamNumber: "14614",
                        AutonScore: 375,
                        TeleScore: 0.0,
                        TotalScore: 94,
                        Record: 0.0
                    },
                    {
                        name: "Lollipop",
                        TeamNumber: "14614",
                        AutonScore: 392,
                        TeleScore: 0.2,
                        TotalScore: 98,
                        Record: 0
                    },
                    {
                        name: "Honeycomb",
                        TeamNumber: "14614",
                        AutonScore: 408,
                        TeleScore: 3.2,
                        TotalScore: 87,
                        Record: 6.5
                    },
                    {
                        name: "Donut",
                        TeamNumber: "14614",
                        AutonScore: 452,
                        TeleScore: 25.0,
                        TotalScore: 51,
                        Record: 4.9
                    },
                    {
                        name: "KitKat",
                        TeamNumber: "14614",
                        AutonScore: 518,
                        TeleScore: 26.0,
                        TotalScore: 65,
                        Record: 7
                    }
                ];
            },

            editItem(item) {
                this.editedIndex = this.Teams.indexOf(item);
                this.editedItem = Object.assign({}, item);
                this.dialog = true;
            },

            deleteItem(item) {
                const index = this.Teams.indexOf(item);
                confirm("Are you sure you want to delete this item?") &&
                this.Teams.splice(index, 1);
            },

            close() {
                this.dialog = false;
                this.$nextTick(() => {
                    this.editedItem = Object.assign({}, this.defaultItem);
                    this.editedIndex = -1;
                });
            },

            save() {
                if (this.editedIndex > -1) {
                    Object.assign(this.Teams[this.editedIndex], this.editedItem);
                } else {
                    this.Teams.push(this.editedItem);
                }
                this.close();
            }
        }
    };
</script>