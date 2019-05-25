<template>
  <div>
    <input type="file" @change="onFileChange">
    <button v-if="data.length >0" @click="loopThrough" >Loop Through Populated Array</button>
  </div>
</template>

<script>
  import XLSX from 'xlsx';

  export default {
    data() {
      return {
        data: []
      }
    },
    methods: {

      onFileChange(e) {
        var files = e.target.files || e.dataTransfer.files;
        if (!files.length)
          return;
        this.processExcel(files[0]);
      },
      processExcel(file) {
        var reader = new FileReader();

        reader.onload = (e) => {
          var data = new Uint8Array(e.target.result);
          var workbook = XLSX.read(data, {type: 'array'});
          var first_sheet_name = workbook.SheetNames[0];
          var worksheet = workbook.Sheets[first_sheet_name];

          let arrayOfRows = XLSX.utils.sheet_to_json(worksheet, {header: 1})

          for(var i = 0; i<= arrayOfRows.length-1; i++) {
            let pObj = {
              surname: `${arrayOfRows[i][0]}`,
              firstname: `${arrayOfRows[i][1]}`,
              lastname: `${arrayOfRows[i][2]}`,
            };

            let centerObj = {
              centername: `${arrayOfRows[i][3]}`
            };

            let artObj = {
              //forgot what the last property name is, hence named it art.
              art: `${arrayOfRows[i][4]}`
            };


            this.data.push([pObj,centerObj, artObj])
          }



        };
        reader.readAsArrayBuffer(file);
      },

      //call axios here to do your magic.
      loopThrough() {
        this.data.forEach(e => {
          //now e is an array of three objects
          console.log(e[0]) //logs the object for surname firstname and lastname.
          console.log(e[1]) //logs the object for center
          console.log(e[2])// logs the object for the last
        })
      }
    }
  }
</script>
