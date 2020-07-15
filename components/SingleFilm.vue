<template>
  <div class="custom-card">
    <div class="custom-card-menu">
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
    </div>
    <img class="img_poster" :src="'https://image.tmdb.org/t/p/w200/' + (item.poster_path != null ? item.poster_path : 'wwemzKWzjKYJFfCeiB57q3r4Bcm.png')" alt="">
    <div>
      <div class="custom-card-average_prosent">
        <ProgressCircle :radius="25" :progress="item.vote_average * 10" :stroke="3" />
        <span class="label">{{ item.vote_average * 10 }}<span class="smaller">%</span></span>
      </div>
    </div>
    <div class="description">
      <span v-if="item.title.length > 20" v-b-tooltip.hover class="description-title" :title="item.title">{{ item.title.slice(0,19) }} ...</span>
      <span v-else class="description-title">{{ item.title }}</span>
      <span class="description-date">{{ new Date(item.release_date).toDateString() }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
      default: () => {}
    }
  }

}
</script>

<style lang="scss" scoped>
  .custom-card {
    position: relative;
    width: 240px;
    margin: 12px 12px;
    border-radius: 10px;
    overflow: hidden;
    box-shadow:  0 0 10px rgba(0,0,0,0.5);
  }

  .img_poster {
    height: 80%;
    width: 100%;
  }

  .description {
    display: flex;
    flex-direction: column;
    margin: 20px 10px;
  }

  .description-title {
    font-weight: 700;
  }

  .description-date {
    font-style: italic;
  }

  .custom-card-menu {
    position: absolute;
    width: 22px;
    height: 22px;
    right: 5px;
    top: 5px;
    background-color: lightgray;
    border-radius: 50%;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }

  .custom-card-menu .dot{
    width: 4px;
    height: 4px;
    margin: 1px;
    background-color:grey;
  }

  .custom-card-average_prosent {
    position: absolute;
    transform: translateY(-25px);
  }

  .label {
    position: absolute;
    transform: translateX(-40px) translateY(11px);
    color: wheat;
  }

</style>
