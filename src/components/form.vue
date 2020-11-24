<template>
  <div class="form">
    <BCard title="Card info">
      <BCardBody>
        <BForm @submit.prevent="onSubmit" @reset="onReset" novalidate>
          <BFormGroup
            label="Enter number card:"
            label-cols-sm="4"
            label-for="crd_number"
            label-size="sm"
            description="Please enter card numbers. Example: 0123-4567-8901-2345."
          >
            <BFormInput
              id="crd_number"
              size="sm"
              v-model="form.card_number"
              type="text"
              placeholder="0000-0000-0000-0000"
              :state="validationCardNumber"
            >
            </BFormInput>
            <BFormInvalidFeedback :state="validationCardNumber"
              >Your must input 12 numbers like example.</BFormInvalidFeedback
            >
            <BFormValidFeedback :state="validationCardNumber"
              >Looks Good.</BFormValidFeedback
            >
          </BFormGroup>

          <BFormGroup
            label="Enter date out:"
            label-cols-sm="4"
            label-for="exp_date"
            description="Please enter expiration date. Example: 08-21."
            label-size="sm"
          >
            <BFormInput
              id="exp_date"
              size="sm"
              v-model="form.exp_date"
              type="text"
              placeholder="00-00"
              :state="validationDate"
            >
            </BFormInput>
            <BFormInvalidFeedback :state="validationDate"
              >Your must input 4 numbers like example.</BFormInvalidFeedback
            >
            <BFormValidFeedback :state="validationDate"
              >Looks Good.</BFormValidFeedback
            >
          </BFormGroup>

          <BFormGroup
            label="Enter cvv:"
            label-cols-sm="4"
            label-for="crd_cvv"
            description="Please enter cvv code. Example 012."
            label-size="sm"
          >
            <BFormInput
              id="crd_cvv"
              size="sm"
              v-model="form.card_cvv"
              type="password"
              :state="validationCVV"
            >
            </BFormInput>
            <BFormInvalidFeedback :state="validationCVV"
              >Your must input 3 numbers like example.</BFormInvalidFeedback
            >
            <BFormValidFeedback :state="validationCVV"
              >Looks Good.</BFormValidFeedback
            >
          </BFormGroup>

          <BButton class="mx-2 mt-2" type="submit" variant="success">
            Submit
          </BButton>
          <BButton type="reset" variant="primary" class="mx-2 mt-2">
            Reset
          </BButton>
        </BForm>
      </BCardBody>
    </BCard>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: {
    validCard: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    form: {
      card_number: "",
      exp_date: "",
      card_cvv: ""
    },
    regExpDict: {
      card_number: /^\d{4}-\d{4}-\d{4}-\d{4}$/,
      exp_date: /^(0\d{1}|1[0-2]{1})-(2\d{1})$/,
      card_cvv: /^\d{3,3}$/
    }
  }),
  computed: {
    validationCardNumber() {
      if (!this.form.card_number) return null;
      return this.regExpDict.card_number.test(this.form.card_number);
    },
    validationDate() {
      if (!this.form.card_number) return null;
      return this.regExpDict.exp_date.test(this.form.exp_date);
    },
    validationCVV() {
      if (!this.form.card_number) return null;
      return this.regExpDict.card_cvv.test(this.form.card_cvv);
    }
  },
  methods: {
    onSubmit() {
      let isValid =
        this.validationCardNumber && this.validationDate && this.validationCVV;

      if (!isValid) return;

      if (!Object.keys(this.validCard).length)
        return this.$emit("notifyMsg", "success");

      let res = Object.entries(this.form).every(
        ([key, val]) => this.validCard[key] === val
      );
      res
        ? this.$emit("notifyMsg", "success")
        : this.$emit("notifyMsg", "danger");
      return;
    },
    onReset() {
      Object.keys(this.form).forEach(item => this.$set(this.form, item, ""));
      this.$emit("notifyMsg", null);
    }
  }
};
</script>

<style lang="scss" scoped>
.card-body {
  padding: 0.5rem;
}
</style>
