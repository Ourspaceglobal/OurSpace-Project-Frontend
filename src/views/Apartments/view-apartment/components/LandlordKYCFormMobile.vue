<template>
  <div id="landlord-kyc-form">
    <b-row>
      <b-col v-for="(kyc, index) in formKycs" :key="index" lg="12">
        <b-form-input
          v-if="kyc.datatype === 'string'"
          v-model="kyc.name"
          :state="kyc.hasError"
          :placeholder="kyc.placeholder"
          class="landlord-kyc-input mt-4"
          size="lg"
        />
        <b-form-input
          v-if="kyc.datatype === 'integer'"
          v-model="kyc.name"
          :state="kyc.hasError"
          :placeholder="kyc.placeholder"
          class="landlord-kyc-input mt-4"
          size="lg"
          type="number"
        />
        <b-form-file
          v-else-if="kyc.datatype === 'file'"
          v-model="kyc.name"
          class="landlord-kyc-file mt-4"
          size="lg"
          :placeholder="kyc.placeholder"
        />
        <b-form-datepicker
          v-else-if="kyc.datatype === 'date'"
          class="landlord-kyc-input"
          v-model="kyc.name"
          size="lg"
        >
        </b-form-datepicker>
        <b-form-timepicker
          v-else-if="kyc.datatype === 'time'"
          class="landlord-kyc-input"
          v-model="kyc.name"
          size="lg"
        >
        </b-form-timepicker>
        <b-form-textarea
          v-else
          v-model="kyc.name"
          class="landlord-kyc-input mt-4"
          size="lg"
          :placeholder="kyc.placeholder"
        />
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  props: ["kycs"],
  data() {
    return {
      formKycs: [],
    };
  },
  methods: {
    validateAndSubmitKysc() {
      this.formKycs = this.formKycs.map((kyc) => {
        if (!kyc.name) {
          kyc.hasError = true;
          kyc.error = `${kyc.placeholder} is required`;
        }
        return kyc;
      });
      if (this.formKycs.find((kyc) => !kyc.name)) {
        return;
      } else {
        this.$emit("validateAndSubmitKysc", this.formKycs);
      }
    },
  },
};
</script>

<style>
#landlord-kyc-form {
  font-family: "Circular Std Book", sans-serif;
  font-weight: normal;
}
.landlord-kyc-input {
  border: none;
  background-color: #f5f4ff;
  border-radius: 6px;
}
.landlord-kyc-input:focus {
  background-color: #f5f4ff;
}
.landlord-kyc-select {
  border: none;
  background-color: #f5f4ff;
  border-radius: 6px;
}
.landlord-kyc-select:focus {
  box-shadow: none;
  border-color: transparent;
}
.custom-file-label {
  border: none;
  background-color: #f5f4ff;
  border-radius: 6px;
}
.custom-file-input:focus {
  box-shadow: none;
  border: none;
}
.custom-file-label::after {
  background-color: transparent;
}
.custom-file-input ~ .custom-file-label[data-browse]::after {
  content: url("../../../../assets/icons/file-upload.svg");
  padding-top: 0.6em;
}
</style>
