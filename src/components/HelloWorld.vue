<template>
 <div class="animated fadeIn">
  <b-row class="justify-content-center" >
  </b-row>
<b-row class="justify-content-center">
  <b-col md="8">
      <div>
    <b-form>

   <b-button type="button" variant="success"  @click="addItem">Add Education</b-button>
<!--added index to track every form with its index.-->
  <mdb-card class="card-body" style="margin-top: 1rem;" v-for="(item, index) in educationForm.education" v-bind:key="item.id">
    <mdb-card-title>Educational Qualification {{index + 1}}
      <button v-if="index != 0" @click="removeEducation(index)" type="button" class="close" aria-label="Close">
      <span aria-hidden="true">×</span>
    </button>
    </mdb-card-title>
<!--made sure every form is bound to its right form object using the index-->
    <div class="flex-row">
       <mdb-input label="School Name" v-model="educationForm.education[index].schoolName" size="lg" required/>
      <mdb-input label="Year Started" v-model="educationForm.education[index].yearStart" size="lg" required/>
      <mdb-input label="Year Ended" v-model="educationForm.education[index].yearEnd" size="lg" required/>
      <mdb-input label="Qualification Earned" v-model="educationForm.education[index].qualificationEarned" size="lg" required/>
    </div>
  </mdb-card>

      <b-button type="button" variant="primary" @click="saveEducation">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>

     <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ educationForm }}</pre>
    </b-card>
  </div>
  </b-col>
  </b-row>
  </div>
</template>

<script>
import { mdbCard, mdbCardBody, mdbCardTitle, mdbCardText, mdbCardGroup, mdbInput } from 'mdbvue';

  export default {

    name: 'new-artisan',
     components: {
      mdbCard,
      mdbCardBody,
      mdbCardGroup,
      mdbCardTitle,
      mdbCardText,
      mdbInput
     },
    data() {

      return {
        educationForm: {
          _id: '',
          education: [{
          schoolName: '',
          yearStart: '',
          yearEnd: '',
          qualificationEarned: ''
          }]
          }
      }

    },
    methods: {
      removeEducation(index) {
        //you can warn the user before remove the education qualification
        this.educationForm.education.splice(index,1)
      },
      saveEducation() {
        //this.educationForm._id = this.personaId;
       // this.addEducation(this.educationForm).then(e => {
       //   this.$bvModal.msgBoxOk('Artisan Profile Education Submited. Click the Next Button to proceed')
       // });
      },
      addItem() {
        this.educationForm.education.push({
          schoolName: this.educationForm.education.schoolName,
          yearStart: this.educationForm.education.yearStart,
          yearEnd: this.educationForm.education.yearEnd,
          qualificationEarned: this.educationForm.education.qualificationEarned
        });
      }

    }

}

</script>
