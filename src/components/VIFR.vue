<template>
  <p>참여 횟수 : {{TryCount}}</p>
  <p>선택 : {{PickValue}}</p>
  <button type="button" @click="onJoinList">참여내역</button>
  <p>당첨명단 : {{PrizeList}}</p>
  <!-- <br/> -->
  <button type="button" @click="onTicket(1)">참여권 1개<br/>1,390 FC/MC <br/>구매하기</button>
  <button type="button" @click="onTicket(3)">참여권 3개 <br/>5,070 FC/MC<br/>구매하기</button>
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
  <button @click="onPointItem(30,$event)">30포인트 <br/>교환하기</button>
  <button @click="onPointItem(20,$event)">20포인트 <br/>교환하기</button>
  <button @click="onPointItem(10,$event)">10포인트 <br/>교환하기</button>
  <button @click="onPointItem(2,$event)">2포인트 <br/>교환하기</button>
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
    let TryCount = ref(0)
    let SSSItem = ref(['','[5강 확률 UP!]22TOTY ALL 강화 선수팩 (1강 ~5강)', '22TOTY, 22TOTY-N, 21UCL Top Price 120 선수팩 (5강, 99+)'])
    let SSItem = ref(['','22TOTY, 22TOTY-N, 21UCL 포함 Top Price 상자 (3,5강)', '[키컨달인] 행운의 BP 카드 (18억 ~ 200억)'])
    let SItem = ref(['','[키컨달인] 프리미엄 고수 상자', '[22TOTY, 21UCL 포함] 최종 OVR 102+ 선수팩 (5강)', '[키컨달인] 행운의 BP 카드 (7억 ~ 90억)'])
    let AItem = ref(['','22TOTY, 22TOTY-N, 21UCL ALL 강화 선수팩 (1강 ~ 5강)', '22TOTY, 22TOTY-N, 21UCL 포함 Top Price 600 선수팩', '[키컨달인] 행운의 BP카드 (4.5억 ~ 30억)'])
    let BItem = ref(['','[키컨달인] Top Price 상자 (최대 8강)', '[EBS 포함] 최종 OVR 102+ 선수팩 (최대 8강)', '[키컨달인] 행운의 BP 카드 (3억 ~ 10억)'])
    let PointItem = ref(['1/N 스페셜판 SSS,SS 상자', '스페셜판 SSS,SS 상자', '스페셜판 SSS,SS,S 상자', '[고수 상자 기회 10%] 행운의 BP 카드 (1억 ~ 5억 BP)'])
    let JoinItem = ref(['[키컨달인] 행운의 BP 카드 (100만 ~ 5억)'])
    let IndemList = ref([])
    let JoinList = ref([])
    let PrizeList = ref([])
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
      TryCount,
      SSSItem,
      SSItem,
      SItem,
      AItem,
      BItem,
      PointItem,
      JoinItem,
      IndemList,
      JoinList,
      PrizeList,
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
        if(this.BingoCount == 6) { //SSS, 완벽한 선방! 
          this.ComValue = '[SSS] 완벽한 선방! '
          this.IndemList[0] = this.SSSItem[Math.ceil(Math.random()*2)]
          this.PrizeList = '피***인 구단주님이 "'+this.IndemList[0]+'" 아이템에 당첨되었습니다.'
        } else if(this.BingoCount == -6) { //SSS, 완벽한 실패..
          this.ComValue = '[SSS] 완벽한 실패.. '
          this.IndemList[0] = this.SSSItem[Math.ceil(Math.random()*2)]
          this.PrizeList = '피***인 구단주님이 "'+this.IndemList[0]+'" 아이템에 당첨되었습니다.'
          // this.IndemList[1] = this.JoinItem[0]
        } else if (this.BingoCount == 4) { //SS, 거의 완벽한 선방! 실패경험치 +1
          this.ComValue = '[SS] 6번 중 5번 성공! '
          this.FailExp += 1
          this.IndemList[0] = this.SSItem[Math.ceil(Math.random()*2)]
          // this.IndemList[1] = this.JoinItem[0]
        } else if (this.BingoCount == -4) { //B, 평균적 선방!  실패경험치 +5
          this.ComValue = '[B] 6번 중 1번 성공! '
          this.FailExp += 5
          this.IndemList[0] = this.BItem[Math.ceil(Math.random()*3)]
          // this.IndemList[1] = this.JoinItem[0]
        } else if (this.BingoCount == 2)  { //S, 성공적 선방! 실패경험치 +2
          this.ComValue = '[S] 6번 중 4번 성공! '
          this.FailExp += 2
          this.IndemList[0] = this.SItem[Math.ceil(Math.random()*3)]
          // this.IndemList[1] = this.JoinItem[0]
        } else if (this.BingoCount == -2)  { //B, 평균적 선방! 실패경험치 +4
          this.ComValue = '[B] 6번 중 2번 성공! '
          this.FailExp += 4
          this.IndemList[0] = this.BItem[Math.ceil(Math.random()*3)]
          // this.IndemList[1] = this.JoinItem[0]
        } else if (this.BingoCount == 0)  { //A, 절반의 선방! 실패경험치 +3
          this.ComValue = '[A] 6번 중 3번 성공! '
          this.FailExp += 3
          this.IndemList[0] = this.AItem[Math.ceil(Math.random()*3)]
          // this.IndemList[1] = this.JoinItem[0]
        }
        alert("서버 : "+this.ResultValue+"\n선택 : "+this.PickValue+"\n비교 : "+this.EqualValue+"\n결과 : "+this.ComValue+"\n보상 : "+this.IndemList)
        this.JoinList += '스페셜 게임 참여 | '+this.ComValue+'\n'+this.IndemList+'\n'
        this.Ticket += -1
        this.BingoCount = 0
        this.EqualValue = []
        this.ComValue = ''
        this.TryCount += 1
        this.IndemList = []
        }
        if (this.FailExp >= 7) {
          this.BonusPoint += 100
          this.FailExp += -7
        }
        this.CheckList = 0
      } 
    },
    onJoinList: function(evt)  { //구분(일반 게임 참여, 일반 참여권 구매), 게임 결과(선방성공 회\n선방실패 회), 획득 아이템, 키컨 포인트(사용), 수령일시(YYYY.MM.DD HH:mm)
      alert(this.JoinList)
    },
    onTicket: function(value,evt) {
      if (value == 1) {
        alert('스페셜 참여권 구매완료')
        this.Ticket += 1
        this.JoinList += '스페셜 참여권 구매 | '+this.JoinItem[0]+'\n'
      } else if (value == 3)  {
        alert('스페셜 참여권 3개 구매완료')
        this.Ticket += 3
        this.JoinList += '스페셜 참여권 3개 구매 | '+this.JoinItem[0]+' 3개 \n'
      }
    },
    onPointItem: function(value, evt)  {
      if (value == 30 && this.BonusPoint >= value)  {
        alert(this.PointItem[0]+' 교환완료')
        this.JoinList += '교환 | '+this.PointItem[0]+' '+this.BonusPoint+'P -> '+(this.BonusPoint-value)+'P\n'
        this.BonusPoint += -value
      } else if (value == 20 && this.BonusPoint >= value) {
        alert(this.PointItem[1]+' 교환완료')
        this.JoinList += '교환 | '+this.PointItem[1]+' '+this.BonusPoint+'P -> '+(this.BonusPoint-value)+'P\n'
        this.BonusPoint += -value
      } else if (value == 10 && this.BonusPoint >= value) {
        alert(this.PointItem[2]+' 교환완료')
        this.JoinList += '교환 | '+this.PointItem[2]+' '+this.BonusPoint+'P -> '+(this.BonusPoint-value)+'P\n'
        this.BonusPoint += -value
      } else if (value == 2 && this.BonusPoint >= value)  {
        alert(this.PointItem[3]+' 교환완료')
        this.JoinList += '교환 | '+this.PointItem[3]+' '+this.BonusPoint+'P -> '+(this.BonusPoint-value)+'P\n'
        this.BonusPoint += -value
      } else {
        alert('포인트가 부족합니다.')
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