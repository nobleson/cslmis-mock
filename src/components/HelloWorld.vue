<template>
 <div class="animated fadeIn">
  <b-row class="justify-content-center" >
  </b-row>
<b-row class="justify-content-center">
  <b-col md="8">
      <div>
    <b-form>
   
   <b-button type="button" variant="success"  @click="addItem">Add Education</b-button>
          
  <mdb-card class="card-body" style="margin-top: 1rem;" v-for="item in educationForm.education" v-bind:key="item.id">
    <mdb-card-title>Educational Qualification</mdb-card-title>

    <div class="flex-row">
       <mdb-input label="School Name" v-model="educationForm.education.schoolName" size="lg" required/> 
      <mdb-input label="Year Started" v-model="educationForm.education.yearStart" size="lg" required/> 
      <mdb-input label="Year Ended" v-model="educationForm.education.yearEnd" size="lg" required/> 
      <mdb-input label="Qualification Earned" v-model="educationForm.education.qualificationEarned" size="lg" required/> 
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