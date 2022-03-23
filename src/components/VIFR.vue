<template>
  <p>{{PickValue}}</p>
  <!-- <p v-if="counter < 5">5보다 작습니다</p> -->
  <!-- <p v-else>5와 같거나 큽니다.</p> -->
  <button type="button" @click="Ticket++">참여권 1개 구매하기</button>
  <button type="button" @click="Ticket+=3">참여권 3개 구매하기</button>
  <br/>
  <button type="button" class="_left_1" @click="onClick('L_1', 1, 2, $event)">니어포스트</button>
  <button type="button" class="_right_1" @click="onClick('R_1', 2, 1, $event)">파포스트</button>
  <br/>
  <button type="button" class="_left_2" @click="onClick('L_2', 1, 2, $event)">니어포스트</button>
  <button type="button" class="_right_2" @click="onClick('R_2', 2, 1, $event)">파포스트</button>
  <br/>
  <button type="button" class="_left_3" @click="onClick('L_3', 1, 2, $event)">니어포스트</button>
  <button type="button" class="_right_3" @click="onClick('R_3', 2, 1, $event)">파포스트</button>
  <br/>
  <button type="button" class="_left_4" @click="onClick('L_4', 1, 2, $event)">니어포스트</button>
  <button type="button" class="_right_4" @click="onClick('R_4', 2, 1, $event)">파포스트</button>
  <br/>
  <button type="button" class="_left_5" @click="onClick('L_5', 1, 2, $event)">니어포스트</button>
  <button type="button" class="_right_5" @click="onClick('R_5', 2, 1, $event)">파포스트</button>
  <br/>
  <button type="button" class="_left_6" @click="onClick('L_6', 1, 2, $event)">니어포스트</button>
  <button type="button" class="_right_6" @click="onClick('R_6', 2, 1, $event)">파포스트</button>
  <br/>
  <button type="button" @click="onRandom">랜덤 선택</button>
  <button type="button" @click="onReset">초기화</button>
  <br/>
  <p>보유 참여권 {{Ticket}}</p>
  <button type="button" @click="onStart">참여하기</button>
  <hr/>
  <br/>
  <p>누적 실패 경험치 {{FailExp}}회(7회) -> 보유 키컨 포인트 {{BonusPoint}}P</p>
  <button @click="onRandom">30포인트 교환하기</button>
  <button @click="reset">20포인트 교환하기</button>
  <button @click="onRandom">10포인트 교환하기</button>
  <button @click="reset">2포인트 교환하기</button>
</template>

<script>
import {ref} from 'vue'
export default {
  // data(){
    
  //   return {
  //   }
  // }
  setup() {
    let Ticket = ref(0)
    let FailExp = ref(0)
    let BonusPoint = ref(0)
    let PickValue = ref([])
    let PickValue1 = ref([])
    let ResultValue = ref([])
    let EqualValue = ref([])
    let BingoCount = ref(0)
    let ComValue = ref('')
    let CheckList = ref(0)
    return {
      Ticket,
      FailExp,
      BonusPoint,
      PickValue,
      ResultValue,
      EqualValue,
      BingoCount,
      PickValue1,
      ComValue,
      CheckList,
    }
  },
  methods: {
    onActive: function(value) {
      document.querySelector(value).classList.toggle('active')
    },
    onClick: function(value, pick, Rpick, evt) {
      for (let i =1; i <=6; i++)  {
        if (value == 'L_'+i)  { //L_1 == L_1
          if (this.PickValue[value[2]-1] == pick) {
            return
          } else if (this.PickValue[value[2]-1] == Rpick) {
            this.onActive('._right_'+i)
          }
          this.onActive('._left_'+i)
          this.PickValue[value[2]-1] = pick
        }
        if (value == 'R_'+i) {
          if (this.PickValue[value[2]-1] == pick) {
            return
          } else if (this.PickValue[value[2]-1] == Rpick) {
            this.onActive('._left_'+i)
          }
          this.onActive('._right_'+i)
          this.PickValue[value[2]-1] = pick
        }
      }
    },
    onRandom: function(evt) {
      evt.preventDefault();
      for(let i=0; i<6; i++) {
        this.PickValue1[i] = Math.ceil(Math.random()*2)
        if(this.PickValue1[i] == 1) {
          this.onClick('L_'+(i+1), 1, 2)
        } else if(this.PickValue1[i] == 2) {
          this.onClick('R_'+(i+1), 2, 1)
        }
      }
    },
    onReset: function(evt)  {
      evt.preventDefault();
      for (let i=0; i<6; i++) {
        if (this.PickValue[i] == 1) {
          this.onActive('._left_'+(i+1))
        } else if (this.PickValue[i] == 2) {
          this.onActive('._right_'+(i+1))
        }
      }
      this.PickValue = []
    },
    onStart: function(evt)  {
      evt.preventDefault();
      if (this.Ticket == 0) {
        alert('참여권을 구매해주세요.')
      } else {
      for (let i=0; i<6; i++) {
        if (this.PickValue[i] == null)  {
          alert((i+1)+"번째 항목이 선택되지 않았습니다.")
          this.CheckList = 1
        }
      }
      if (this.CheckList == 0) {
        for(let i=0; i<6; i++) {
        this.ResultValue[i] = Math.ceil(Math.random()*2)
          if(this.ResultValue[i] == this.PickValue[i]) {
            this.EqualValue[i] = 'O'
            this.BingoCount += 1
            } else {
            this.EqualValue[i] = 'X'
            this.BingoCount += -1
          }
        }
        if (this.FailExp == 6) {
          this.BonusPoint += 1
          this.FailExp += -7
        }
        if(this.BingoCount == 6 || this.BingoCount == -6) {
          this.ComValue = '빙고'
        } else if (this.BingoCount == 4) {
          this.ComValue = '6번중 5번성공'
        } else if (this.BingoCount == -4) {
          this.ComValue = '6번중 1번성공'
        } else if (this.BingoCount == 2)  {
          this.ComValue = '6번중 4번성공'
        } else if (this.BingoCount == -2)  {
          this.ComValue = '6번중 2번성공'
        } else if (this.BingoCount == 0)  {
          this.ComValue = '6번중 3번성공'
        }
        if(this.EqualValue != '빙고')  { //구매기회 +2
          this.FailExp += 1
        }
        alert("서버 : "+this.ResultValue+"\n선택 : "+this.PickValue+"\n결과 : "+this.EqualValue+"\n비교 : "+this.ComValue)
        this.Ticket += -1
        this.BingoCount = 0
        this.EqualValue = []
        this.ComValue = ''
        }
        this.CheckList = 0
      } 
    }
  },
}
</script>

<style>
:root {
--text-color: black;
--click-color: red;
}
._left_1  {
  color: var(--text-color);
}
._left_1.active  {
  color: var(--click-color);
}
._right_1  {
  color: var(--text-color);
}
._right_1.active  {
  color: var(--click-color);
}

._left_2  {
  color: var(--text-color);
}
._left_2.active  {
  color: var(--click-color);
}
._right_2  {
  color: var(--text-color);
}
._right_2.active  {
  color: var(--click-color);
}

._left_3  {
  color: var(--text-color);
}
._left_3.active  {
  color: var(--click-color);
}
._right_3  {
  color: var(--text-color);
}
._right_3.active  {
  color: var(--click-color);
}

._left_4  {
  color: var(--text-color);
}
._left_4.active  {
  color: var(--click-color);
}
._right_4  {
  color: var(--text-color);
}
._right_4.active  {
  color: var(--click-color);
}

._left_5  {
  color: var(--text-color);
}
._left_5.active  {
  color: var(--click-color);
}
._right_5  {
  color: var(--text-color);
}
._right_5.active  {
  color: var(--click-color);
}

._left_6  {
  color: var(--text-color);
}
._left_6.active  {
  color: var(--click-color);
}
._right_6  {
  color: var(--text-color);
}
._right_6.active  {
  color: var(--click-color);
}


</style>