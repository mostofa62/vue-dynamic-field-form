<template>
  <div id="visa">
    <h1>RAMMPS Number of Death Application</h1>
    <form @submit.prevent="postData()">
        
      <label for="duration">Number of Inputs:</label>
      <input v-model="n_of_death"  type="text" @change="addVisa" required>
     <br><br>
      Array: {{ applicants.length }}
      Input: {{ n_of_death }}
      <br>
      <div class="name"
      v-for="(applicant, counter) in applicants"
      v-bind:key="counter">
        <span @click="deleteVisa(counter)">x</span>
        <label for="duration">{{counter+1}}. Name:</label>
        <input type="text" v-model.lazy="applicant.name" required>
        <label for="duration">Year of relation:</label>
        <input type="text" v-model.lazy="applicant.relation" required> 
      </div>

      <button type="submit">
        Submit
      </button>
    </form>

  </div>
</template>

<script>
export default {
  name: 'Test',
  props: {
    msg: String
  },
  data(){
    return {
     applicants:[],
     n_of_death:0     
    }
  },

  created() {
    
    this.loadVisa();
  },

  methods : {
    addVisa(){

      let cp = this;
      if(cp.p_n_of_death <1) {
        cp.applicants = [];
      }
      if(cp.n_of_death > 0){

        var n = Math.abs(cp.n_of_death - cp.applicants.length);
        


        for( var i=0;i<n;i++){
          this.applicants.push({
            name:'',
            relation: ''
          })
        }
      }
    },
    deleteVisa(counter){
      let cp = this;
      if(cp.n_of_death > 0){
        cp.n_of_death -= 1;
      }
      this.applicants.splice(counter,1);

    },

    loadVisa(){
      let cp = this;
      if(cp.n_of_death > 0){
        for( var i=0;i<cp.n_of_death;i++){
          cp.applicants.push({
            name:'name_'+i,
            relation: 'relation_'+i
          });
        }
      }

    },

    postData(){
      alert(JSON.stringify(this.applicants));
    }


  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#visa {
  margin: 20px auto;
  max-width: 700px;
}
label{
  display: block;
  margin: 20px 0 10px;
}
input {
  font-size: 30px;
  border: 1px double rgb(102, 97, 96) ;
  border-radius: 4px;
}
button {
  font-size: 16px;
 background: rgb(64, 179, 140);
  padding: 0.4rem 1.3rem;
  text-align: center;
  border: none;
  cursor: pointer;
  border-radius: 4px;
 margin: 10px;
}
span{
  width: 30px;
  float: right;
  cursor: pointer;
}
span:hover{
  color: brown;
}
.name{
  border: 1.5px solid;
  padding:5px;
  margin-bottom: 10px;
}
</style>
