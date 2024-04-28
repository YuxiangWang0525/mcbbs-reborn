<script>
import swal from 'sweetalert'
export default {
  data() {
    return {
      gridSize: 5,
      cellSize: 50,
      letters: ['M', 'C', 'B', 'S'],
      excludeLetter: '',
      moves: 0,
      board: []
    };
  },
  mounted() {
    this.excludeLetter = this.letters[Math.floor(Math.random() * this.letters.length)];
    this.drawBoard();
  },
  methods: {
    drawBoard() {
      const canvas = document.getElementById('chessboard');
      const ctx = canvas.getContext('2d');
      for (let i = 0; i < this.gridSize; i++) {
        this.board[i] = [];
        for (let j = 0; j < this.gridSize; j++) {
          this.board[i][j] = '';
          ctx.strokeRect(i * this.cellSize, j * this.cellSize, this.cellSize, this.cellSize);
        }
      }
    },
    drawLetter(x, y, letter) {
      const canvas = document.getElementById('chessboard');
      const ctx = canvas.getContext('2d');
      ctx.font = '36px serif';
      ctx.fillText(letter, x * this.cellSize + 10, y * this.cellSize + 40);
    },
    checkWin() {
      // 在这里添加胜利条件检测
    },
    handleCanvasClick(event) {
      if (this.moves >= 8) {
        swal('游戏结束','寄,你没能帮助MCBBS打赢复活赛','error');
        return;
      }

      const canvas = document.getElementById('chessboard');
      const rect = canvas.getBoundingClientRect();
      const x = Math.floor((event.clientX - rect.left) / this.cellSize);
      const y = Math.floor((event.clientY - rect.top) / this.cellSize);

      if (!this.board[x][y]) {
        const availableLetters = this.letters.filter(letter => letter !== this.excludeLetter);
        const randomLetter = availableLetters[Math.floor(Math.random() * availableLetters.length)];

        this.drawLetter(x, y, randomLetter);
        this.board[x][y] = randomLetter;
        this.moves++;
        this.checkWin();
      }
    }
  }
};
</script>

<template>
  <div class="mcbbs_gray_background_vuejs_reset"></div>
  <div id="bettersweet_main_container" class="container">
    <div class="text">
      <h1 style="color:#4caf50;font-weight: 500;">MCBBS浴火重生计划</h1>
      <h3>
        回来吧，MCBBS😫<br>
        我最骄傲的信仰😎<br>
        历历在目的限制搜索🥰<br>
        眼泪莫名在流淌😭<br>
        依稀记得我用挖掘卡<br>
        还有珍贵的MC币🥵<br>
        为原本免费的资源付费😋<br>
        就算被Ban也不流泪😏
      </h3>
      <h2>尝试凑齐“MCBBS”以帮助MCBBS打赢复活赛</h2>
      <canvas id="chessboard" width="250" height="250" @click="handleCanvasClick"></canvas>
      <hr>
      <h2>请关注<a href="#bs_vueapp">此页面</a>或<a href="https://mcbbs.rip/">晋级赛</a>获得最新的消息</h2>
      <div align="center">
        <p>2024© mcbbs-reborn <a href="https://yuxiangwang0525.com" target="_blank">Presented by 晚江右海</a></p>
        <p>由<a href="https://cn.vuejs.org" target="_blank">Vue.js</a>强力驱动</p>
        <img src="https://badges.toozhao.com/badges/01HWHQBHYFSFQEBABKKAZ66BQ4/green.svg" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.mcbbs_gray_background_vuejs_reset{
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #fafafa;
  object-fit: cover;
  z-index: -10;
}
h2, h3, h4 {
  font-weight: 300;
}
a[href] {
  color: #4caf50;
  text-decoration: none;
}
</style>
