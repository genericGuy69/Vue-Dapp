<template>
  <section id='signup'>
    <v-layout row>
    <v-flex xs12 sm6 offset-sm3>
    <v-card>
      <v-card-title primary-title>
        <div>
          <div class="headline">Sign up</div>
          <span class="grey--text">Prereqs</span>
        </div>
      </v-card-title>

       <v-card-text>
        <ul>
          <li>Metamask --- Turns your normal chrome/firefox browser into an ethereum browser</li>
          <li>Ether --- New metamask accounts come with ether by default, but otherwise go to ropsten test faucet.</li>
        </ul>

       <form class="form">
          <v-layout row wrap>
            <v-flex xs5 offset-xs1>
              <!-- <button @click="addtodo" name="addtodo">Add Item</button> -->
              <!---<input name="todo" v-model="form.todo"> -->
              <!--<label for="todo">Todo</label> -->
              <v-text-field
                  v-model="form.pseudo"
                  :rules="nameRules"
                  label="Username"
                  required
              ></v-text-field>
            </v-flex>
            <v-flex xs2 offset-xs1>
              <v-btn depressed color="primary" @click="signup" name="addusername">Sign Up</v-btn>
            </v-flex>
          </v-layout>
        </form>
      </v-card-text>

      <v-card-actions>
          <v-btn flat color="orange" href="https://metamask.io/" target="_blank">Metamask</v-btn>
          <v-btn flat color="purple" href="https://faucet.metamask.io/" target="_blank">Ropsten Test Faucet</v-btn>
          <v-spacer></v-spacer>
          <v-btn icon @click="show = !show">
            <v-icon>{{ show ? 'keyboard_arrow_down' : 'keyboard_arrow_up' }}</v-icon>
          </v-btn>
      </v-card-actions>
       <v-slide-y-transition>
          <v-card-text v-show="show">
            I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
          </v-card-text>
      </v-slide-y-transition>

    </v-card>
    </v-flex>
    </v-layout>

    <br />
   </section>
</template>

<script>
  import Users from '@/js/users'

  export default {
    name: 'signup',
    data () {
      return {
        form: {
          pseudo: undefined
        },
        nameRules: [
          v => !!v || 'Name is required',
          v => v.length <= 15 || 'Name must be less than 15 characters'
        ],
        show: false
      }
    },
    beforeCreate: function () {
      Users.init()
    },
    methods: {
      signup: function () {
        let self = this
        if (typeof this.form.pseudo !== 'undefined' && this.form.pseudo !== '') {
          Users.create(this.form.pseudo).then(tx => {
            console.log(tx)
            self.$router.push('/')
          }).catch(err => {
            console.log(err)
          })
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .mybutton {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 14px;
    -webkit-transition-duration: 0.4s; /* Safari */
    transition-duration: 0.4s;
    cursor: pointer;
}

  .mybutton {
      background-color: white; 
      color: black; 
      border: 2px solid #4CAF50;
  }

  .mybutton:hover {
      background-color: #4CAF50;
      color: white;
  }

  #signup {
    text-align: center;
    .simple-form input {
      margin: 0 .25rem;
      min-width: 125px;
      border: 1px solid #eee;
      border-left: 3px solid;
      border-radius: 5px;
      transition: border-color .5s ease-out;
    }
    .simple-form input:optional {
      border-left-color: #4CAF50;
    } 
  }

</style>
