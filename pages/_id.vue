<template>
  <div v-if="tank" class="tank-details">
        <div class="title-thumb">
            <img class="details-flag" :title="tank.country" :src="tank.country_flag" :alt="tank.country"/>
            <h2 class="details-title">{{tank.name.toString().toUpperCase()}} (level {{tank.level}})</h2>
        </div>
        <div class="details-thumb">
            <div class="details-image-thumb">
                <h4 class="details-caption">Preview</h4>
                <img class="details-preview" :src="tank.tank_image" :alt="tank.name"/>
            </div>
            <div class="details-table-thumb">
                <h4 class="details-caption">Characteristics</h4>
                <table class="details-table">
                    <tr class="details-row">
                        <td class="details-cell">damage</td>
                        <td class="details-cell">{{tank.damage}}</td>
                    </tr>
                    <tr class="details-row">
                        <td class="details-cell">breoning</td>
                        <td class="details-cell">{{tank.armor_penetration}}</td>
                    </tr>
                    <tr class="details-row">
                        <td class="details-cell">attack speed</td>
                        <td class="details-cell">{{tank.attack_speed}}</td>
                    </tr>
                    <tr class="details-row">
                        <td class="details-cell">time of tarfeting</td>
                        <td class="details-cell">{{tank.time_of_targeting}}</td>
                    </tr>
                    <tr class="details-row">
                        <td class="details-cell">ammunition</td>
                        <td class="details-cell">{{tank.ammunition}}</td>
                    </tr>
                </table>
            </div>
        </div>
        
        <nuxt-link class="details-btn" to="/">Back to list view</nuxt-link>
    </div>
</template>

<script lang="ts">
import { Context } from '@nuxt/types'

export default {
  async asyncData(context: Context) {
    const id = context.params.id;

    try {
      const tank = await context.$axios.$get(`https://tanks-proj.herokuapp.com/tanks/${id}`);
      return {tank};
    } catch (e) {
      console.log(e)
    }
  }
}
</script>

<style scoped>
root {
    margin: 0;
    padding: 0;
}

* {
    background-color: #212020;
    color: #b3a6a6;
}

.tank-details {
  height: 100vh;
  padding: 40px;
}

.details-thumb {
    display: flex;
    align-items: flex-start;
}

.details-table-thumb, .details-image-thumb {
    width: 40%;
}

.title-thumb{
    display: flex;
    align-items: center;
    margin-bottom: 40px;
}

.details-flag {
    margin-right: 10px;
}

.details-btn {
    display: block;
    background-color: transparent;
    border: none;
    cursor: pointer;
}

.details-table {
    width: 100%;
    border-collapse: collapse;
}

.details-cell {
    padding: 7px;
    border: 1px solid #b3a6a6;
}

.details-caption {
  margin-bottom: 20px;
}

</style>