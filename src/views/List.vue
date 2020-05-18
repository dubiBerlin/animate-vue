<template>
  <div style="width:70%; margin:0 auto;">
    <input type="text" v-model="newContact" placeholder="Name" />
    <button @click="addContact">Add Contact</button>
    <button @click="blinkList">Blink</button>
    <transition name="fade">
      <div v-show="isError" class="error">
        <span>{{ this.newContact }}</span> allready exists in the list
      </div>
    </transition>

    <ul>
      <li
        v-for="contact in contacts"
        :key="contact.name"
        :class="{ errorli: contact.isDuplicate }"
      >
        {{ contact.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      duplicateContact: "",
      newContact: "",
      contacts: [
        {
          name: "Beau Thabeast",
          isDuplicate: false,
          blink: false
        },
        {
          name: "Alice Vunderlind",
          isDuplicate: false,
          blink: false
        },
        {
          name: "Cindy Rella",
          isDuplicate: false,
          blink: false
        }
      ],
      liErrorClass: "error-li",
      blinkClass: "blink",
      blink: false,
      isError: false
    }
  },
  watch: {
    newContact: function(newValue, oldValue) {
      if (this.isError) {
        this.isError = newValue != oldValue ? false : true
        this.duplicateContact.isDuplicate = false
        this.duplicateContact = ""
      }
    }
  },
  methods: {
    blinkList() {
      console.log("blinkList() ", this.blink)
      // this.blink = true
    },
    addContact() {
      if (this.newContact.length == 0) {
        return
      } 

      let contact = this.contacts.find(
        contact => contact.name == this.newContact
      )
      if (contact === undefined) {
        this.contacts.push({
          name: this.newContact,
          isDuplicate: false,
          blink: false
        })
        this.newContact = ""
      } else {
        this.isError = true
        contact.isDuplicate = true
        this.duplicateContact = contact
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

.errorli {
  background-color: crimson;
  color: #eee;
  transition: all 1s;
}

.errorli:hover {
  color: #eee;
  border-color: crimson;
}

.blink {
  border-color: goldenrod;
  background-color: gold;
  color: #000;
  transition: all 0.2s;
}

li {
  background-color:white;
  width: 30%;
  margin: 5px auto 0 auto;
  padding: 5px;
  border: 1px solid transparent;
  border-radius: 5px;
  color: #000;
}

li:hover {
  border-color: #eee;
  color: darkgray;
  transition: all 0.2s;
}
</style>