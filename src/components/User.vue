<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: {{ name }}</p>
    <p>{{ getDateAndTime(createdAt) }}</p>
    {{ helloToMixin }} {{test}}
    <v-btn color="info" @click="changeName()">이름 변경</v-btn>
    <hr>

    <v-layout >
      <v-flex xs12 sm6>
        <UserDetail 
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
        >
        </UserDetail>
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
          @child="parents"
        ></UserEdit>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import UserDetail from "./UserDetail.vue"
import UserEdit from "./UserEdit.vue"
import { dateFormat } from "../mixins/dateFormat"

export default {
  components: {
    UserDetail,
    UserEdit
  },
  data() {
    return {
      name: 'Hoza',
      address: 'Seoul',
      phone: '1234-4567',
      hasDog: true,
      createdAt: null,
    }
  },
  computed:{
    helloToMixin() {
      return this.mixinData + " 안녕하세요"
    },
    test() {
      let a = "가나다"
      a = "abc"
      return a
    }
  },
  created() {
    console.log("메인");
    this.createdAt = new Date()
  },
  methods:{
    changeName() {
      this.name = "Hoza"
    },
    parents(user) {

      this.name=user.name
      this.address=user.address
      this.phone=user.phone
      this.hasDog=user.hasDog

      console.log("부모가 받았어")
    },
    getDateAndTime(date){
      let hour = date.getHours()
      let minutes = date.getMinutes()
      let fullDate =  `${date.getFullYear()}/${date.getMonth()+1}/${date.getDate()}`
      return `${fullDate} ${hour}:${minutes}`
    }
  },
  mixins: [dateFormat]
}
</script>