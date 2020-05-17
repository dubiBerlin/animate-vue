<template>
  <div>
    <input type="text" v-model="newContact" placeholder="Name" />
    <button @click="addContact">Add Contact</button>
    <transition name="fade">
      <div v-show="isError" class="error">
        <span>{{ this.newContact }}</span> allready exists in the list
      </div>
    </transition>

    <ul>
      <li v-for="contact in contacts" :key="contact">
        {{ contact }}
      </li>
    </ul>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      isError: false,
      newContact: "",
      contacts: ['Beau Thabeast', 'Cindy Rella', 'Alice Vunderlind']
    }
  },
  methods: {
    addContact() {
      if(this.newContact.length == 0){
        return;
      } 
      if(this.contacts.find(contact => contact==this.newContact) === undefined){
        this.contacts.push(this.newContact)
        this.newContact = ""
        this.isError = false
      }else{
        this.isError = true
      }
    }
  }
}
</script>
<style>
.error {
  color: crimson;
  font-size: 14px;
  font-weight: 700;
  text-align: center;
  border: 1px solid crimson;
  border-radius: 5px;
  padding: 10px;
  margin-top: 10px;
  width: 50%;
  margin: 0 auto;
}

.error > span {
  font-weight: 900;
}
</style>