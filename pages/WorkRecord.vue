<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-card>
          <v-card-text>
            <v-form ref="form" v-model="valid" lazy-validation>
              <v-menu
                v-model="menu2"
                :close-on-content-click="false"
                :nudge-right="40"
                transition="scale-transition"
                offset-y
                min-width="auto"
              >
                <template #activator="{ on, attrs }">
                  <v-text-field
                    v-model="date"
                    label="日期"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker
                  v-model="date"
                  @input="menu2 = false"
                ></v-date-picker>
              </v-menu>
              <v-select
                v-model="work_unit_input"
                :items="work_units"
                :rules="[(v) => !!v || 'Item is required']"
                label="工作單位"
                required
              ></v-select>
              <v-select
                v-model="customers_input"
                :items="customers"
                :rules="[(v) => !!v || 'Item is required']"
                label="客戶"
                required
              ></v-select>
              <v-select
                v-model="project_type_input"
                :items="project_types"
                :rules="[(v) => !!v || 'Item is required']"
                label="專案項目"
                required
              ></v-select>
              <v-textarea
                v-model="work_description"
                name="work_desciption"
                label="工作描述"
              ></v-textarea>
              <v-text-field
                v-model="work_spend_time_input"
                label="工作時數"
              ></v-text-field>
            </v-form>
            <v-btn class="mr-4" @click="submit"> 送出 </v-btn>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      {{ work_records.date }}
      {{ work_records.work_unit }}
      {{ work_records.customer }}
      {{ work_records.project_type }}
      {{ work_records.work_description }}
      {{ work_records.work_spend_time_input }}
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    work_unit_input: null,
    customers_input: null,
    project_type_input: null,
    work_description: null,
    work_spend_time_input: null,
    work_units: ['業務', '專案', '營運', '行政', '行銷'],
    customers: ['IBA', 'RK', 'DGPR', 'Linker', 'MACUS', '再生緣', '台灣萊雅'],
    project_types: ['seo', '廣告', '社群', '網站設計', '口碑'],
    date: new Date().toISOString().substr(0, 10),
    menu: false,
    menu2: false,
    work_records: {
      date: '',
      work_unit: '',
      customer: '',
      project_type: '',
      work_description: '',
      work_spend_time_input: '',
    },
  }),
  methods: {
    submit() {
      this.work_records.date = this.date
      this.work_records.work_unit = this.work_unit_input
      this.work_records.customer = this.customers_input
      this.work_records.project_type = this.project_type_input
      this.work_records.work_description = this.work_description
      this.work_records.work_spend_time_input = this.work_spend_time_input
    },
  },
}
</script>
