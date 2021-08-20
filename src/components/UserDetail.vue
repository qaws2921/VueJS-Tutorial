<template>
  <div class="red lighten-3 pa-3">
    <h3>자세한 회원 정보를 확인합니다.</h3>
    <p>상세사항</p>
    <v-list dense>
      <v-list-item-title>
        <v-list-item-action>이름:</v-list-item-action>
        <v-list-item-action class="align-end">
          {{ name }}
        </v-list-item-action>
      </v-list-item-title>
      <v-list-item-title>
        <v-list-item-action>주소:</v-list-item-action>
        <v-list-item-action class="align-end">
          {{ address }}
        </v-list-item-action>
      </v-list-item-title>
            <v-list-item-title>
        <v-list-item-action>전화번호:</v-list-item-action>
        <v-list-item-action class="align-end">
          {{ phone }}
        </v-list-item-action>
      </v-list-item-title>
      <v-list-item-title>
        <v-list-item-action>반려견유무:</v-list-item-action>
        <v-list-item-action class="align-end">
          {{ hasDogKr }}
        </v-list-item-action>
      </v-list-item-title>
      <v-list-item-title>
        <v-list-item-title>수정일자:</v-list-item-title>
        <v-list-item-title class="align-end">
          {{ getDateAndTime(editedDate) }}
        </v-list-item-title>
      </v-list-item-title>
    </v-list>
    
  </div>
</template>
<script>
import { eventBus } from "../main"
import { dateFormat } from "../mixins/dateFormat"


export default {
  data() {
    return {
      editedDate: null
    }
  },
  props:['name','address','phone','hasDog'],
  // props:{
  //   nameOfChild: {
  //     type: String,
  //     default: 'LEGO'
  //   }
  // },
  computed: {
    hasDogKr() {
      return this.hasDog === true ? '있음' : '없음'
    },
    sayHllo () {
      return this.nameOfChild+ ' 안녕하세요.'
    }
  },
  methods: {
    switchName () {
      this.nameOfChild = '컴퓨터'
    },
    // getDateAndTime(date){
    //   if(date !== null) {
    //     let hour = date.getHours()
    //     let minutes = date.getMinutes()
    //     let fullDate =  `${date.getFullYear()}/${date.getMonth()+1}/${date.getDate()}`
    //     return `${fullDate} ${hour}:${minutes}`
    //   } else {
    //     return null
    //   }
      
    // }
  },
  created() {
        console.log("디테일");
    eventBus.$on('userWasEdited', date => {
        console.log(date)
        this.editedDate = date
    })
  },
  mixins: [dateFormat]
}
</script>