<template>
  <div class="tank-thumb" title="Click to details">
    <img class="tank-preview" :src="tankItem.tank_image" :alt="tankItem.name"/>
    <div class="tank-preview-info-thumb">
        <img class="tank-flag" :title="tankItem.country" :src="tankItem.country_flag" :alt="tankItem.country"/>
        <p class="tank-level">{{tankItem.level}}</p>
        <p class="tank-name" :title="tankItem.name.toString().toUpperCase()">{{tankItem.name.toString().toUpperCase()}}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
      tankItem: {
        type: Object,
        required: true
      }
  }
}

</script>

<style scoped>
.tank-preview {
    display: block;
    margin-right: auto;
    margin-left: auto;
    width: 100%;
    height: auto;
}

.tank-preview-info-thumb {
    display: grid;
    
    grid-template-columns: 2fr 1fr 1fr 3fr 2fr;
    
    align-items: center;
    justify-items: center;

    margin-right: auto;
    margin-left: auto;
    padding: 20px 0;
}

.tank-name {
    width: 100%;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

.tank-flag {
    grid-column-start: 2;
}

.tank-thumb:hover * {
    background-color: #3a5243;
}
</style>
