<template>
  <div style="width:70%; margin:0 auto;">
    <input type="text" v-model="newContact" placeholder="Name" />
    <button @click="addContact">Add Contact</button>
    <button @click="startBlinking">Blink</button>
    <transition name="fade">
      <div v-show="isError" class="error">
        <span>{{ this.newContact }}</span> allready exists in the list
      </div>
    </transition>

    <ul>
      <li
        v-for="contact in contacts"
        :key="contact.name"
        :class="[{ errorli: contact.isDuplicate }, { blink: contact.blink }]"
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
      isError: false,
      timeout: ""
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
    startBlinking() {
      if (this.contacts.length == 0) {
        return
      }
      this.addBlinkClass(this.contacts, 0)
    },
    addBlinkClass(contacts, index) {
      contacts[index].blink = true

      this.timeout = setTimeout(() => {
        contacts[index].blink = false
        if (contacts.length - 1 >= index + 1) {
          index = index + 1
          this.addBlinkClass(contacts, index)
        } else {
          clearTimeout(this.timeout)
        }
      }, 500)
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
  color: #dc3545;
  font-size: 14px;
  font-weight: 700;
  text-align: center;
  border: 1px solid #dc3545;
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
  background-color: #dc3545;
  color: #eee;
  transition: all 1s;
}

.errorli:hover {
  color: #eee;
  border-color: #dc3545;
}

.blink {
  border-color: goldenrod;
  background-color: gold;
  color: #000;
  transition: all 2s;
}

li {
  background-color:white;
  width: 30%;
  margin: 5px auto 0 auto;
  padding: 5px;
  border: 1px solid transparent;
  border-radius: 5px;
  color: #000;
  transition: all 2s;
}

li:hover {
  border-color: #eee;
  color: darkgray;
  transition: all 0.2s;
}
</style>