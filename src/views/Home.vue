<template>
  <div class="home">
    <h2>Enter the amount of color codes you want in the json file<span class="primary">.</span></h2>
    <div class="input">
      <input type="number" placeholder="Amount of color codes" v-model="amount" />
      <button @click="generateFile()">
        <svg width="24" height="24" fill="none" viewBox="0 0 24 24">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4.75 14.75V16.25C4.75 17.9069 6.09315 19.25 7.75 19.25H16.25C17.9069 19.25 19.25 17.9069 19.25 16.25V14.75"></path>
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 14.25L12 4.75"></path>
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M8.75 10.75L12 14.25L15.25 10.75"></path>
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data: () => {
    return {
      amount: null,
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
      if(this.amount > 0) {
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
      } else {
        alert('You need to give a number higher than 0')
      }
    },
  },
};
</script>

<style lang="scss">
  .home {
    position: relative;
    display: inline-block;
    h2 {
      text-align: center;
      color: #f1f1f1;
    }
    .primary {
      color: #6037f3;
    }

    .input {
      display: flex;
      justify-content: center;
      margin: 0 auto;

      input {
        border: 2px solid #6037f3;
        padding: 7px 15px 10px 15px;
        font-size: 16px;
        border-radius: 20px 0px 0px 20px;
        font-family: inherit;

        &:focus {
          outline: none;
        }
      }

      button {
        background-color: #6037f3;
        border: none;
        border-radius: 0px 20px 20px 0px;
        padding: 10px 10px 7px 7px;
        cursor: pointer;
        font-size: 14px;
        font-family: inherit;
        color: #f1f1f1;
      }
    }
  }
</style>
