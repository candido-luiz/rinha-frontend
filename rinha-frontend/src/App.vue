<template>
  <div class="start-container">
    <h1 class="application-name">JSON Tree Viewer</h1>
    <div class="application-description">
      Simple JSON Viewer that runs completely on-client. No data exchange
    </div>
    <div>
      <button class="load-json-button">Load JSON</button>
    </div>
    <div class="invalid-file-message">
      Invalid file. Please load a valid JSON file.
    </div>
  </div>
</template>

<script>

</script>

<style>
.start-container{
  display: flex;
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
}
.invalid-file-message{
  color: #BF0E0E;
  font-family: Inter;
  font-size: 16px;
  font-style: normal;
  font-weight: 400;
  line-height: normal; 
}
</style>