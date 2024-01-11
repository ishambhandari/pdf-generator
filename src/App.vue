<template>
  <div class="app">
    <div class="custom-div">
      <img src="./assets/oncalogo.png" alt="Dummy Logo" class="dummy-logo" />
      <h1 class="heading">PDF generator</h1>

      <div class="container mt-5 font-style">
        <div class="row">
          <div class="col-md-6 offset-md-3">
            <form>
              <div class="mb-3">
                <label for="exampleFormControlInput1" class="form-label"
                  >Title</label
                >
                <input
                  v-model="title"
                  type="text"
                  class="form-control"
                  id="exampleFormControlInput1"
                />
              </div>
              <div class="mb-3">
                <label for="exampleFormControlTextarea1" class="form-label">
                  Descripton</label
                >
                <textarea
                  v-model="description"
                  class="form-control"
                  id="exampleFormControlTextarea1"
                  rows="3"
                ></textarea>
              </div>

              <button
                @click="downloadPDF"
                type="submit"
                class="btn btn-primary"
              >
                Export PDF
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { jsPDF } from "jspdf";
export default {
  name: "app",
  data() {
    return {
      title: "",
      description: "",
    };
  },
  methods: {
    downloadPDF() {
      let pdf = new jsPDF();
      let width = pdf.internal.pageSize.getWidth();
      let height = pdf.internal.pageSize.getHeight();
      console.log("title", this.title);
      pdf.addImage(
        "https://i.ibb.co/MMkFgw4/Onca-monthly-report.png",
        "PNG",
        0,
        0,
        width,
        height
      );
      pdf.addPage();
      pdf.text(this.title, 10, 10);
      pdf.text(this.description, 10, 20);
      pdf.save("test.pdf");
    },
  },
};
</script>

<style>
#app {
  text-align: center;
}

.custom-div {
  background-color: black;
  padding: 20px;
  position: relative;
}
.heading {
  color: #fff;
}

.dummy-logo {
  width: 100px; /* Adjust the width as needed */
  height: auto;
  position: absolute;
  top: 10px;
  left: 10px;
}
.font-style {
  color: #fff;
}
</style>
