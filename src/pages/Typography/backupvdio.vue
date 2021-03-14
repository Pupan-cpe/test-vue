<template>
  <div>
    <v-dialog
      v-model="this.$store.getters.stateDialogFarm"
      persistent
      :overlay="false"
      max-width="80%"
      transition="dialog-transition"
    >
      <v-card style="border-radius:10px 10px 0px 0px">
        <v-toolbar
          style="background-color:#1EC384;border-radius:10px 10px 0px 0px ;;color:#FFFFFF"
          class="pa-0"
          >เพิ่มฟาร์ม <v-spacer></v-spacer>
        </v-toolbar>
        <br />
        <template>
          <a-form-model
            :model="form"
            :label-col="labelCol"
            :wrapper-col="wrapperCol"
          >
            <a-form-model-item label="ชื่อฟาร์ม">
              <a-input
                v-model="form.farm"
                type="name"

                :rules="[rules.req]"
              />
            </a-form-model-item>
            <a-form-model-item label="ชื่อ-นามสกุล เจ้าของฟาร์ม">
              <a-input v-model="form.name" />
            </a-form-model-item>
            <a-form-model-item label="เลขบัตรประชาชน">
              <a-input v-model="form.idcard" />
            </a-form-model-item>
            <a-form-model-item label="เลขที่ทะเบียนฟาร์ม">
              <a-input v-model="form.idfarm" />
            </a-form-model-item>
            <a-form-model-item label="มาตรฐานฟาร์ม">
              <a-checkbox-group v-model="form.type">
                <a-checkbox value="1" name="type">
                  CoC
                </a-checkbox>
                <a-checkbox value="2" name="type">
                  GAP
                </a-checkbox>
                <a-checkbox value="3" name="type">
                  new GAP
                </a-checkbox>
                <a-checkbox value="4" name="type">
                  BAP
                </a-checkbox>
                <a-checkbox value="5" name="type"> อื่นๆ </a-checkbox
                ><Input placeholder="other" id="other"  v-model="form.other"/>
              </a-checkbox-group>
            </a-form-model-item>
            <a-form-model-item label="ที่อยู่">
              <a-input v-model="form.address" />
            </a-form-model-item>

            <a-form-model-item label="จังหวัด">
              <a-select
                :default-value="provinceData[0]"
                style="width: 120px"
                @change="handleProvinceChange"
              >
                <a-select-option
                  div v-for="province in provinceData"
                
                  :key="province"
                >
                  {{ province }}
                </a-select-option>
              </a-select>

              อำเภอ:
              <a-select v-model="secondCity" style="width: 120px">
                <a-select-option v-for="city in cities" :key="city">
                  {{ city }}
                </a-select-option>
              </a-select>

              ตำบล:
              <a-select v-model="district1" style="width: 120px">
                <a-select-option v-for="district in district" :key="district">
                  {{ district }}
                </a-select-option>
              </a-select>
            </a-form-model-item>
          </a-form-model>
        </template>

        <v-container>
          <v-btn
            class="mr-4"
            outlined
            color="success"
            @click="$store.dispatch('closeDialogFarm')"
            >บันทึก</v-btn
          >
          <v-btn
            class="mr-4"
            outlined
            color="error"
            @click="$store.dispatch('closeDialogFarm')"
            >ยกเลิก</v-btn
          >
        </v-container>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
const provinceData = ['ทดสอบA', 'ทดสอบB']
const cityData = {
  ทดสอบA: ['Aทดสอบ1', 'Aทดสอบ2', 'Aทดสอบ3'],
  ทดสอบB: ['Bทดสอบ1', 'Bทดสอบ2', 'Bทดสอบ3']
}
const district = {
  ทดสอบA: ['C1', 'C2', 'C3'],
  ทดสอบB: ['D1', 'D2', 'D3']
}
export default {
  data () {
    return {
      rules: {
        req: value => !!value || 'จำเป็นต้องใส่ข้อมูล.'
      },
      provinceData,
      cityData,
      district,

      cities: cityData[provinceData[0]],
      secondCity: cityData[provinceData[0]][0],
      district1: district[provinceData[0]][0],
      labelCol: { span: 5 },
      wrapperCol: { span: 14 },
      form: {
        name: '',
        farm: '',
        idcard: '',
        idfarm: '',
        address: '',
        other: '',

        type: [],
        resource: '',
        desc: ''
      }
    }
  },
  methods: {
    handleProvinceChange (value) {
      this.cities = cityData[value]
      this.district = district[value][0][1][2]
      this.secondCity = cityData[value][0]
    }
  }
}
</script>

<style lang="scss" scoped></style>
