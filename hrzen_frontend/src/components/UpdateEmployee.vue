<template>
  <v-dialog v-model="localDialog" max-width="500px">
    <v-card>
      <v-card-title>
        <span class="headline">Edit Employee</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="6" md="4">
              <v-text-field v-model="localEmployee.name" label="Name"></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field v-model="localEmployee.position" label="Position"></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field v-model="localEmployee.salary" label="Salary" type="number"></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="4">
              <v-text-field v-model="localEmployee.email" label="Email"></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn class="cancel-btn" text @click="closeDialog">Cancel</v-btn>
        <v-btn class="save-btn" text @click="updateEmployee">Save</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import axios from 'axios';
import { useToast } from 'vue-toast-notification';

export default {
  name: 'UpdateEmployee',
  props: {
    dialog: {
      type: Boolean,
      required: true
    },
    employee: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      localDialog: this.dialog,
      localEmployee: { ...this.employee }
    };
  },
  watch: {
    dialog(val) {
      this.localDialog = val;
    },
    localDialog(val) {
      this.$emit('update:dialog', val);
    },
    employee(val) {
      this.localEmployee = { ...val };
    }
  },
  methods: {
    closeDialog() {
      this.localDialog = false;
    },
    updateEmployee() {
  const toast = useToast();
  const token = localStorage.getItem('token');
  axios.put(`https://hr-system-wcp8.onrender.com/api/employees/${this.localEmployee.id}`, this.localEmployee, {
    headers: {
      'Authorization': `Bearer ${token}`
    }
  })
    .then(() => {
      this.$emit('employee-updated');
      toast.success('Employee updated successfully!');
      this.closeDialog();
    })
    .catch(error => {
      toast.error('There was an error updating the employee!');
      console.error("There was an error updating the employee!", error);
    });
  }
  
    // updateEmployee() {
    //   const toast = useToast();
    //   axios.put(`https://hr-system-wcp8.onrender.com/api/employees/${this.localEmployee.id}`, this.localEmployee)
    //     .then(() => {
    //       this.$emit('employee-updated');
    //       toast.success('Employee updated successfully!');
    //       this.closeDialog();
    //     })
    //     .catch(error => {
    //       toast.error('There was an error updating the employee!');
    //       console.error("There was an error updating the employee!", error);
    //     });
    // }
  }
};
</script>
<style scoped>
.cancel-btn {
  background-color: #E0E1DD !important;
  color: #415A77 !important;
}
.save-btn {
  background-color: #778DA9 !important;
  color: white !important;
}
.v-card-title{
  background-color: #1B263B;
  color: #E0E1DD;
}
</style>