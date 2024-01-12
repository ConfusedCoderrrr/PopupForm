<script>
import { ref, watch } from 'vue';

const dialogVisible = ref(false);

const ruleName = ref('');
const expression = ref('');
const period = ref('');
const silencePeriod = ref('');
const message = ref('');
const storedData = ref([]);
const runIs = ref(false);
const exIs = ref(false);
const perIs = ref(false);
const silIs = ref(false);
const mesIs = ref(false);
let valper = ref(false);
let valper1 = ref(false);
let valstr = ref(false);
let valstr1 = ref(false);

const handleAdd = () => {
  const regex = /\d/;
  const test1 = regex.test(ruleName.value);
  const test2 = regex.test(message.value);


  const regex1 = /^\d+$/;
  const test3 = !regex1.test(period.value);
  const test4 = !regex1.test(silencePeriod.value);





  if (test1 || test2 || test3 || test4 || ruleName.value === "" || expression.value === "" || period.value === "" || silencePeriod.value === "" || message.value === "") {
    if (test1 && ruleName.value !== "") {
      valstr.value = true;
    }
    if (test2 && message.value !== "") {
      valstr1.value = true;
    }
    if (test3 && period.value !== "") {
      valper.value = true;
    }
    if (test4 && silencePeriod.value !== "") {
      valper1.value = true;
    }
    if (ruleName.value === "") {
      runIs.value = true;

    }
    if (expression.value === "") {
      exIs.value = true;

    }
    if (period.value === "") {
      perIs.value = true;

    }
    if (silencePeriod.value === "") {
      silIs.value = true;

    }
    if (message.value === "") {
      mesIs.value = true;

    }
    return;
  }

  else {
    console.log("rule name: " + ruleName.value);
    console.log("expression: " + expression.value);
    console.log("period: " + period.value + 'Ms');
    console.log("silencePeriod: " + silencePeriod.value + 'Ms');
    console.log("message: " + message.value);
    const newData = {
      ruleName: ruleName.value,
      expression: expression.value,
      period: period.value,
      silencePeriod: silencePeriod.value,
      message: message.value,
    };

    storedData.value.push(newData);

    console.log("previous data", storedData.value);

    ruleName.value = '';
    expression.value = '';
    period.value = '';
    silencePeriod.value = '';
    message.value = '';

    return;
  }
};


</script>

<script setup>
import { ElMessageBox } from 'element-plus'





</script>
<template>
  <el-button text @click="dialogVisible = true">
    click to open the Dialog
  </el-button>
  <div style="height: 100%; width: 100%; display: flex; align-items: center; justify-content: center;">
    <el-dialog v-model="dialogVisible" width="451px" hight="72px"
      style="padding: 0px; margin-top: 1.5%; margin-bottom: 1.5%;">




      <template #header>
        <div style="height: 72px; display:flex; align-items: center; color:font-family: Inter;
         font-size: 18px;
         font-style: normal;
         font-weight: 600;
         line-height: normal;
         background-color:#0E0032;
         color: #F8F8F8;">
          Add alert
        </div>
      </template>

      <form action="">
        <div class="formDiv" style="padding-top: 0px; padding-bottom: 0px;">
          <input @focus="runIs = false, valstr = false" class="inputBox" v-model="ruleName" placeholder="Rule name"
            type="text" :style="{ borderColor: runIs ? 'red' : 'initial' }">
          <p v-if="runIs" class="alertD">Please enter rule name first</p>
          <p v-if="valstr" class="alertD">Please enter valid name</p>

          <input @focus="exIs = false" class="inputBox" v-model="expression" placeholder="Expression" type="text"
            :style="{ borderColor: exIs ? 'red' : 'initial' }">

          <p v-if="exIs" class="alertD">Please enter expression first</p>

          <input @focus="perIs = false, valper = false" class="inputBox" v-model="period" placeholder="Period" type="text"
            :style="{ borderColor: perIs ? 'red' : 'initial' }">

          <p v-if="perIs" class="alertD">Please enter period first</p>
          <p v-if="valper" class="alertD">Please enter valid period, it should only contain nubmers</p>

          <input @focus="silIs = false, valper1 = false" class="inputBox" v-model="silencePeriod"
            placeholder="Silence period" type="text" :style="{ borderColor: silIs ? 'red' : 'initial' }">
          <p v-if="silIs" class="alertD">Please enter silence period first</p>
          <p v-if="valper1" class="alertD">Please enter valid silence period, it should only contain nubmers</p>

          <textarea @focus="mesIs = false, valstr1 = false" v-model="message" placeholder="Message" id="textArea"
            cols="30" rows="10" :style="{ borderColor: mesIs ? 'red' : 'initial' }"></textarea>
          <p v-if="mesIs" class="alertD">Please enter message first</p>
          <p v-if="valstr1" class="alertD">Please enter valid message, it should not contain numbers</p>
        </div>
      </form>

      <template #footer>
        <span class="dialog-footer">
          <el-button type="primary" @click="handleAdd"
            style="background-color: #E0E4E8; border: none; color: #000088; width:64px; height: 35px;">
            Add
          </el-button>
        </span>
      </template>
    </el-dialog>
  </div>
</template>


<style scoped>
.dialog-footer button:first-child {
  margin-right: 10px;
}

.inputBox {
  padding-left: 10px;
  margin-top: 12px;
  width: 398px;
  height: 56px;
  flex-shrink: 0;
  border-radius: 5px;
  border: 0.5px solid #8D8E90;
  background: #FFF;
  font-size: 16px;

}

#textArea {
  padding-left: 10px;
  padding-top: 10px;
  padding-bottom: 10px;
  margin-top: 12px;
  width: 398px;
  border-radius: 5px;
  border: 0.5px solid #8D8E90;
  background: #FFF;
  font-size: 16px;
  height: 138px;
}

.alertD {
  color: rgb(171, 48, 48);
}
</style>
