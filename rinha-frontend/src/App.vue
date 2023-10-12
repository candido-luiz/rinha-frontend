<template>
  <div v-if="!fileContent" class="start-container">
    <h1 class="application-name">JSON Tree Viewer</h1>
    <div class="application-description">
      Simple JSON Viewer that runs completely on-client. No data exchange
    </div>
    <div>
      <button @click="triggerFileInput" class="load-json-button">Load JSON</button>
    </div>
    <div v-if="invalidFile" class="invalid-file-message">
      Invalid file. Please load a valid JSON file.
    </div>
    <input 
      ref="fileInput" 
      class="hiddenInput" 
      type="file" 
      name="jsonFile" 
      id="json_file_input"
      @change="handleFile"
    >
  </div>
  <div v-else class="start-container">
    <ul>
      <div v-if="Array.isArray(fileContent)">
      
        <TreeTest
          v-for="(viewItem, index) in fileContent"
          :key="index"
          :itemContent="viewItem"
          :itemIndex="index"
        />
      
      </div>

      <div v-else>
        <TreeTest
          :itemContent="fileContent"
        />
      </div>
    </ul>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import TreeTest from "./components/TreeTest.vue";

const invalidFile = ref(false);
const fileInput = ref(null);
const fileContent = ref(null);
const selectedFileName = ref("");

watch(fileContent, (newFileContent) => {
  console.log(newFileContent)
  console.log(JSON.stringify(newFileContent))
})

function triggerFileInput(){
  const inputElement = fileInput.value;
  if(inputElement) {
    inputElement.click();
  }
}

function handleFile(){
  const files = fileInput.value.files || [];
  if(files.length){
    const selectedFile = files[0];
    const fileBlob = new Blob([selectedFile], {type: "application/json"})

    const fr = new FileReader();

    fr.onload = function() {
      if(this.result){
        try {
          const parsedFile = JSON.parse(this.result);
          fileContent.value = parsedFile;
          invalidFile.value = false;
        }
        catch(error){
          console.error(error);
          invalidFile.value = true;
          fileContent.value = null;
        }
      }
    }

    fr.readAsText(fileBlob)

    selectedFileName.value = selectedFile?.name;
  }
}

</script>

<style>
.start-container{
  display: flex;
  min-height: 100vh;
  padding: 102px 46px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 24px; 
}
.application-name{
  color: #000;
  font-family: Inter;
  font-size: 48px;
  font-style: normal;
  font-weight: 700;
  line-height: normal; 
}
.application-description{
  color: #000;
  font-family: Inter;
  font-size: 24px;
  font-style: normal;
  font-weight: 400;
  line-height: normal; 
}
.load-json-button{
  color: #000;
  font-family: Inter;
  font-size: 16px;
  font-style: normal;
  font-weight: 500;
  line-height: normal;
  border-radius: 5px;
  /* border: 1px solid #000;
  opacity: 0.7;
  background: linear-gradient(180deg, #E4E4E4 0%, #F7F7F7 100%); */
}
.invalid-file-message{
  color: #BF0E0E;
  font-family: Inter;
  font-size: 16px;
  font-style: normal;
  font-weight: 400;
  line-height: normal; 
}
.hiddenInput{
  display: none;
}
</style>