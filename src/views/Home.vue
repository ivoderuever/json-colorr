<template>
  <div class="home">
    <input type="number" placeholder="amount" v-model="amount" />
    <button @click="generateFile()">Generate</button>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data: () => {
    return {
      amount: 0,
      colors: []
    };
  },
  methods: {
    randomColor() {
      return "#000000".replace(/0/g, function () {
        return (~~(Math.random() * 16)).toString(16);
      });
    },
    generateFile() {
      //generated given amount of color codes
      for(let i = 0; i < this.amount; i++ ) {
        this.colors.push(this.randomColor());
      }
      console.log(this.colors);

      //creates file and enables dowload of set file
      const data = JSON.stringify({colors: this.colors})
      const blob = new Blob([data], {type: 'text/plain'})
      const e = document.createEvent('MouseEvents'),
      a = document.createElement('a');
      a.download = "colors.json";
      a.href = window.URL.createObjectURL(blob);
      a.dataset.downloadurl = ['text/json', a.download, a.href].join(':');
      e.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
      a.dispatchEvent(e);

      //clear colors array
      this.colors = []
    },
  },
};
</script>

<style lang="scss">
</style>
