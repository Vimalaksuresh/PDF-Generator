<template>
    <div class="mainbody">
      <form @submit.prevent="generatePDF">
        <div class="mb-3">
          <label class="form-label">Name:</label>
          <input type="text" class="form-control" v-model="formData.name">
        </div>
        <div class="mb-3">
          <label class="form-label">Age</label>
          <input type="text" class="form-control" v-model="formData.age">
        </div>
        <div class="mb-3">
          <label class="form-label">Insurer</label>
          <input type="text" class="form-control" v-model="formData.insurer">
        </div>
        <div class="mb-3">
          <label class="form-label">Plan</label>
          <input type="text" class="form-control" v-model="formData.plan">
        </div>
        <div class="mb-3">
          <label class="form-label">Rider</label>
          <input type="text" class="form-control" v-model="formData.rider">
        </div>
  
        <button type="submit" class="btn btn-primary">Generate PDF</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        formData: {
          name: '',
          age: '',
          insurer: '',
          plan: '',
          rider: ''
        }
      };
    },
    methods: {
  async generatePDF() {
    try {
      // Replace with your actual form data
      const formData = {
        name: 'John Doe',
        date: 'September 9, 2024',
        // Add other fields as needed
      };

      const response = await axios.get('https://script.google.com/macros/s/AKfycbwww_ojqduDtMz-mFj3n2iS_yy5Z9rbEXagO_D61k6rE5Pig1CSGCd7e_lYiBAuKgFp/exec', formData, {
        headers: {
          'Content-Type': 'application/json'
        }
      });

      console.log('PDF generated successfully:', response.data);

      // Check if the response contains the URL of the generated PDF
      if (response.data && response.data.url) {
        // Optionally, open the generated PDF in a new tab
        window.open(response.data.url, '_blank');
      } else {
        console.error('No URL found in the response data:', response.data);
      }
    } catch (error) {
      console.error('Error generating PDF:', error);
    }
  }
}

  };
  </script>
  
  <style scoped>
  .mainbody {
    max-width: 600px;
    margin: auto;
    padding: 20px;
  }
  </style>
  