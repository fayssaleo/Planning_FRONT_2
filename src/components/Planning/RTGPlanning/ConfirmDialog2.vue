<template>
  <v-dialog height="100%">
    <v-card>
      <v-card-title>Selected Items</v-card-title>

      <v-card-text>
        <!-- Drivers -->
        <v-row>
          <v-col cols="6" style="border-right: 1px solid #2196f3">
            <v-row class="">
              <v-col cols="12" class="driverListTitle"
                >Driver listc({{ driverCount }}) :
              </v-col>
              <v-col cols="12" style="border-top: 1px solid #4f7cac">
                <v-row style="padding: 1px" class="mt-2 driverLst">
                  <v-col
                  cols="1" md="3" sm="3"
                    v-for="driver in selectedDrivers"
                    :key="driver.id"
                  >
                    <span
                      class="CheckedButton"
                      :class="
                        driver.selected
                          ? 'CheckedButtonSelected'
                          : 'CheckedButtonNotSelected'
                      "
                      @click="driver.selected = !driver.selected"
                      >{{ driver.firstname[0].toUpperCase()+driver.firstname.slice(1) }}<br /> {{ driver.lastname.toUpperCase() }}  <br />
                      <span style="font-weight: bold; font-size: 14px"
                        >({{ driver.workingHours }}wh)</span
                      ></span
                    >
                  </v-col>
                </v-row>
              </v-col>
            </v-row>
          </v-col>
          <v-col cols="6">
            <v-row class="">
              <v-col cols="12" class="EquipmentListTitle"
                >Equipment list ({{ equipmentCount }}) :
              </v-col>
              <v-col cols="12" style="border-top: 1px solid #4f7cac">
                <v-row style="padding: 1px" class="mt-2 driverLst">
                  <v-col
                  cols="1" md="3" sm="3"
                    v-for="equipment in equipmentList"
                    :key="equipment.id"
                  >
                    <span
                      class="CheckedButton"
                      :class="
                        equipment.selected
                          ? 'CheckedButtonSelectedEquipment'
                          : 'CheckedButtonNotSelected'
                      "
                      @click="equipment.selected = !equipment.selected"
                      >{{ equipment.matricule }}</span
                    >
                  </v-col>
                </v-row>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-card-text>

      <!-- Dialog actions -->
      <v-card-actions class="dialogActions">
        <v-btn
          density="default"
          style="background-color: #15263f; color: white; width: 120px"
          @click="validateSelections"
          >Confirm</v-btn
        >
        <v-btn @click="closeDialog">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: ["selectedDrivers", "equipmentList", "driverCount", "equipmentCount"],

  computed: {},

  methods: {
    validateSelections() {
      // Perform validation or further actions here
      this.$emit("validateSelections"); // Emit a custom event to notify the parent component
    },

    closeDialog() {
      this.$emit("closeDialog"); // Emit an update event to synchronize the dialog prop with the parent
    },

    removeDriver(driver) {
      this.$emit("removeDriver", driver);
    },

    removeEquipement(equ) {
      this.$emit("removeEquipement", equ);
    },
  },
};
</script>

<style scoped>
.header {
  width: 100%;
  background-color: #f5f5f5; /* Light gray background */
  border-bottom: 2px solid #4f7cac; /* Bottom border */
  padding: 5px 10px; /* Padding for spacing */
  text-align: center; /* Center align the text */
  font-size: 15px; /* Increase font size */
  font-weight: bold; /* Bold text */
  margin-bottom: 0.2rem; /* Space below the header */
}
.block {
  border: 1px solid #4f7cac;
  margin-top: 5px;
}
.selectAll {
  display: inline-block;
  color: white;
  font-family: sans-serif;
  font-size: 15px;
  text-align: center;
  border-radius: 9px;
  cursor: pointer;
  user-select: none;
  max-height: 62px;
  /* position: relative; */
  float: right;
  margin-right: 40px;
  width: 200px;
  height: 29px;
  margin-top: 4px;
  margin-right: 5px;
  padding-top: 3px;
}
.selectAll:hover {
  opacity: 0.8;
}
.selectAll:active {
  opacity: 0.5;
}
.CheckedButton {
  padding-top: 3px;
  color: white;
  font-family: sans-serif;
  font-size: 17px;
  text-align: center;
  border-radius: 9px;
  cursor: pointer;
  user-select: none;
  position: relative;
  display: inline-block;
  width: 100%;
  font-weight: bold;
  margin-top: -12px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
.CheckedSelectButtonSelected {
  background-color: #4169E1;
}
.CheckedSelectButtonNotSelected {
  color: rgb(196 113 113);
    border: 1px solid rgb(196 113 113);
}
.CheckedButtonSelected {
  background-color: #4169E1;
}
.CheckedButtonSelectedEquipment {
  background-color: #52ad9c;
}
.CheckedButtonNotSelected {
  color: rgb(196 113 113);
    border: 2px solid rgb(196 113 113);
}
.CheckedButton:hover {
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
  transform: translateY(-2px);
}
.CheckedButton:active {
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
  transform: translateY(-4px);
}
.driverLst {
  padding: 1px;
  max-height: 727px;
  overflow: scroll;
}

.tableHeader {
  height: 60px;
}
.driverListTitle {
  font-size: 26px;
  color: #4f7cac;
  margin-left: 13px;
  font-weight: bold;
  position: relative;
}
.EquipmentListTitle {
  font-size: 26px;
  color: #52ad9c;
  margin-left: 13px;
  font-weight: bold;
  position: relative;
}
.driverListTitle::after {
  content: "\F05D2"; /* mdi-left-arrow icon */
  font-family: "Material Design Icons"; /* Ensure this matches your mdi font family */
  position: absolute;
  right: 18px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 25px; /* Adjust size as necessary */
  font-weight: 100 !important;
}
.EquipmentListTitle::after {
  content: "\F0DD1"; /* mdi-left-arrow icon */
  font-family: "Material Design Icons"; /* Ensure this matches your mdi font family */
  position: absolute;
  right: 18px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 25px; /* Adjust size as necessary */
  font-weight: 100 !important;
}
</style>
