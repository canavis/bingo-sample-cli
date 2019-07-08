<template>
  <div v-if="!isStartBingo">
    <p>Set MAX Number</p>
    <p><input type="number" v-model="maxNumber" id="max-number" class="input"></p>
    <p v-if="maxNumberValidationError" class="error-text">Set a value between 1 and less than 100.</p>
    <button v-on:click="setNumber" class="btn btn--information btn-set-number">Set number</button>
  </div>
</template>

<script>
export default {
  name: 'SetNumber',
  data () {
    return {
      maxNumber: 500,
      shuffleNumber: 0,
      chosenNumber: [],
      remainNumber: [],
      maxNumberValidationError: false,
      isStartBingo: false,
      isFinishBingo: false,
      isShuffle: false,
    }
  },
  // props: {
  //   maxNumber: String,
  //   shuffleNumber: String,
  //   chosenNumber: Array,
  //   remainNumber: Array,
  //   maxNumberValidationError: Boolean,
  //   isStartBingo: Boolean
  // },
  methods: {
    setNumber: function() {
      // 最大番号セット
      this.maxNumber = Number(this.maxNumber);

      // 番号バリデーション
      if (this.maxNumber < 1 || this.maxNumber > 101) {
        this.maxNumberValidationError = true;
        return;
      } else {
        this.maxNumberValidationError = false;
      }

      // 番号セット完了
      this.isStartBingo = true;

      // 番号管理オブジェクト生成
      for (let i = 0; i < this.maxNumber; i++) {
        this.chosenNumber.push({
          id: Number([i]) + 1,
          isHit: false
        });
      }

      // ルーレット用番号生成
      for (let i = 0; i < this.maxNumber; i++) {
        this.remainNumber[i] = i + 1
      }
      this.startShuffle();
    }
  }
}
</script>

<style>

</style>
