<template>
  <div class="digitalScroll">
    <div style="height: 22px; overflow: hidden">
      <div class="frame" style="margin-left: 10px"></div>
      <ul ref="ul">
        <li>0</li>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
        <li>9</li>
        <li>0</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
ul {
  list-style: none;
  margin-left: -30px;
}
.digitalScroll {
  width: 200px;
  height: 500px;
  //   background-color: antiquewhite;
  display: flex;
  flex-direction: column;
  align-items: center;
  .frame {
    width: 20px;
    height: 20px;
    border: 1px solid black;
  }
  ul {
    animation: move 1s linear infinite;
  }
  @keyframes move {
    from {
      transform: translateY(-90%);
      filter: url(#blur);
    }
    to {
      transform: translateY(1%);
      filter: url(#blur);
    }
  }
}
</style>
