<template>
  <div class="song-list">
    <ul>
      <li @click="selectItem(item,index)" v-for="(item,index) of songs" class="item">
        <div class="rank" v-show="rank">
          <span :class="getRankCls(index)" v-text="getRankText(index)"></span>
        </div>
        <div class="content">
          <h2 class="name">{{item.name}}</h2>
          <p class="desc">{{getDesc(item)}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: ["songs", "rank"],
  methods: {
    getDesc(item) {
      // if (typeof item.album !== "object") {
      return item.singer;
      // }
      // return `${item.singer}·${item.album}`;
    },
    selectItem(item, index) {
      this.$emit("select", item, index);
    },
    getRankCls(index) {
      if (index <= 2) {
        return `icon icon${index}`;
      } else {
        return `text`;
      }
    },
    getRankText(index) {
      if (index > 2) {
        return index + 1;
      }
    }
  }
};
</script>
<style lang="stylus" scoped>
@import '~common/stylus/variable';
@import '~common/stylus/mixin';

.item {
  display: flex;
  align-items: center;
  box-sizing: border-box;
  height: 64px;
  font-size: $font-size-medium;

  .rank {
    flex: 0 0 25px;
    width: 25px;
    margin-right: 30px;
    text-align: center;

    .icon {
      display: inline-block;
      width: 25px;
      height: 24px;
      background-size: 25px 24px;

      &.icon0 {
        bg-image('first');
      }

      &.icon1 {
        bg-image('second');
      }

      &.icon2 {
        bg-image('third');
      }
    }

    .text {
      color: $color-theme;
      font-size: $font-size-large;
    }
  }

  .content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    line-height: 20px;
    overflow: hidden;

    .name {
      no-wrap();
      color: #fff;
    }

    .desc {
      no-wrap();
      margin-top: 4px;
      color: hsla(0, 0%, 100%, 0.3);
    }
  }
}
</style>