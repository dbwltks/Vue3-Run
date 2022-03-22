<template>
  <p>{{PickValue}}</p>
  <p v-if="counter < 5">5보다 작습니다</p>
  <p v-else>5와 같거나 큽니다.</p>
  <button type="button" @click="Ticket++">참여권 1개 구매하기</button>
  <button type="button" @click="Ticket+=3">참여권 3개 구매하기</button>
  <br/>
  <button type="button" class="_left" @click="onClick('L_1', $event)">니어포스트</button>
  <button type="button" class="_right" @click="onClick('R_1', $event)">파포스트</button>
  <br/>
  <button type="button" @click="onClick('L_2', $event)">니어포스트</button>
  <button type="button" @click="onClick('R_2', $event)">파포스트</button>
  <br/>
  <button type="button" @click="onClick('L_3', $event)">니어포스트</button>
  <button type="button" @click="onClick('R_3', $event)">파포스트</button>
  <br/>
  <button type="button" @click="onClick('L_4', $event)">니어포스트</button>
  <button type="button" @click="onClick('R_4', $event)">파포스트</button>
  <br/>
  <button type="button" @click="onClick('L_5', $event)">니어포스트</button>
  <button type="button" @click="onClick('R_5', $event)">파포스트</button>
  <br/>
  <button type="button" @click="onClick('L_6', $event)">니어포스트</button>
  <button type="button" @click="onClick('R_6', $event)">파포스트</button>
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
    return {
      Ticket,
      FailExp,
      BonusPoint,
      PickValue,
    }
  },
  methods: {
    onClick: function(value, evt) {
      switch(value) {
        case 'L_1':
          // evt.preventDefault();
          this.PickValue[0] = 1
          if(this.PickValue[0] == 1) {
            alert('니어포스트 1')
            document.querySelector('._left').classList.toggle('active')
          } if (document.querySelector('._right').classList.toggle('active'))  {
          document.querySelector('._right').classList.toggle('active')
          }
          break
        case 'R_1':
          this.PickValue[0] = 2
          if(this.PickValue[0] == 2) {
            alert('파포스트 1')
            document.querySelector('._right').classList.toggle('active')
          } if (document.querySelector('._left').classList.toggle('active'))  {
          document.querySelector('._left').classList.toggle('active')
          }
          break
        case 'L_2':
          alert('니어포스트 2')
          this.PickValue[1] = 1
          break
        case 'R_2':
          alert('파포스트 2')
          this.PickValue[1] = 2
          break
        case 'L_3':
          alert('니어포스트 3')
          this.PickValue[2] = 1
          break
        case 'R_3':
          alert('파포스트 3')
          this.PickValue[2] = 2
          break
        case 'L_4':
          alert('니어포스트 4')
          this.PickValue[3] = 1
          break
        case 'R_4':
          alert('파포스트 4')
          this.PickValue[3] = 2
          break
        case 'L_5':
          alert('니어포스트 5')
          this.PickValue[4] = 1
          break
        case 'R_5':
          alert('파포스트 5')
          this.PickValue[4] = 2
          break
        case 'L_6':
          alert('니어포스트 6')
          this.PickValue[5] = 1
          break
        case 'R_6':
          alert('파포스트 6')
          this.PickValue[5] = 2
          break
        default:
          alert('오류')
          break
      }
    },
    onRandom: function(evt) {
      evt.preventDefault();
      for(let i=0; i<6; i++) {
        this.PickValue[i] = Math.ceil(Math.random()*2)
        this.onClick(L_i)
      }
    },
    onReset: function(evt)  {
      evt.preventDefault();
      this.PickValue = []
    },
    onStart: function(evt)  {
      evt.preventDefault();
      if (this.Ticket == 0) {
        alert('참여권을 구매해주세요.')
      } else if (this.PickValue == 0) {
        alert('선택 해주세요')
      } else {
        alert('참여완료')
        this.Ticket += -1
      }
    }
  },
}
</script>

<style>
._left  {
  color: black;
}
._left.active  {
  color: red;
}
._right  {
  color: black;
}
._right.active  {
  color: red;
}

</style>