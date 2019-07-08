<template>
  <div v-if="isStartBingo">
    <div v-if="!isFinishBingo">
      <p v-if="isShuffle"><button v-on:click="stopShuffle" class="btn btn--information">STOP!</button></p>
      <p v-if="!isShuffle"><button v-on:click="startShuffle" class="btn btn--information">SPIN!</button></p>
    </div>
    <p class="choice-number">{{ shuffleNumber }}</p>
    <ul class="number-list">
      <li v-for="(item, index) in chosenNumber" v-bind:class="[item]">{{ item.id }}</li>
    </ul>
    <button onclick="location.reload();" class="btn btn--small btn--danger btn-reset">Reset</button>
  </div>
</template>

<script>
export default {
  name: 'NumberList',
  props: {
    shuffleNumber: 0,
    chosenNumber: [],
    remainNumber: [],
    isStartBingo: false,
    isFinishBingo: false,
    isShuffle: false,
  },
  choiceNumber: function () {
    // 残り番号からランダムに選択
    let random = Math.floor(Math.random() * this.remainNumber.length);
    return this.remainNumber[random];
  },
  startShuffle: function () {
    // ビンゴシャッフル表示
    this.isShuffle = true;
    shuffleTimer = setInterval(function () {
      const random = Math.floor(Math.random() * this.remainNumber.length);
      this.shuffleNumber = this.remainNumber[random];
    }.bind(this), 20);
  },
  stopShuffle: function() {
    // STOPボタン押下時

    // 選択された番号を取得
    const random = this.choiceNumber();

    // 出た玉の情報を更新
    for (let i = 0; i < this.chosenNumber.length; i++) {
      // 過去に選択されているかチェック
      if (this.chosenNumber[i].id === random) {
        if (this.chosenNumber[i].isHit) {
          // もう一度番号を選択する
          this.choiceNumber();
        } else {
          // 選択済みに更新
          this.chosenNumber[i].isHit = true;
        }
      }
    }

    // シャッフル停止
    clearInterval(shuffleTimer);
    this.isShuffle = false;
    for (let i = 0; i < this.remainNumber.length; i++) {
      if (this.remainNumber[i] === random) {
        // 選択されたデカ番号表示
        this.shuffleNumber = this.remainNumber[i]
        // 残り番号配列から削除
        this.remainNumber.splice(i, 1);
      }
    }

    // 残り玉が 0 の場合
    if (this.remainNumber.length <= 0) {
      this.shuffleNumber = 'complete!'
      this.isFinishBingo = true;
    }
  }
}
</script>

<style>

</style>
