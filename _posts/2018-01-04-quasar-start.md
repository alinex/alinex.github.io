---
title: First Quasar Application
layout: post
tags: JavaScript Vue Quasar
---

After decifing to make my next frontend using quasar I first had to read through the
following documentations in about 2 days:

- [Vue.js](https://vuejs.org/v2/guide/installation.html) as the base technology for the client interface
- [vue-router](https://router.vuejs.org/en/) for client side routing
- [Quasar Framework](http://quasar-framework.org/guide/) components and base structure with electron and cordova integration
- [Vuelidate](https://monterail.github.io/vuelidate/#getting-started) for form validation
- [Axios](https://github.com/axios/axios) HTTP client library
- [JWT](https://jwt.io/#debugger) JSON Web Token for authentication
- [Stylus](http://stylus-lang.com/) CSS language

It looks a lot but most stuff is real easy so you may go along very fast and come
back to these pages while working with it.

# Starter

I used the _default_ Quasar starter kit and first made some layout changes to get
ajusted with the framework. My next step was to build a simple layout and checkout
the electron wrapper which works really good.

I added some npm scripts to call everything I need.

# The Application

My first application should not be any hello world fuss but a really functioning
and usable application so I created:

> [Alinex Admin Portal](https://github.com/alinex/quasar-admin) which should be used
as frontend to different administration tasks

# Integrate Authentication

My next Task was to add authentication to the client. This is not as easy because I had to think of a way to check that other pages should be only visible if authenticated and make methods which will later connect to the server for the authentication.

## Routing

To work with these I made the following routes:

The default route giving a welcome page if nothing is select and user is not authenticated.

    { path: '/', component: load('welcome/welcome'), beforeEnter: checkAuth },

Load the login or register pages with a special layout.

    {
      path: '/',
      component: load('layouts/auth'),
      children: [
        { path: 'login', component: load('auth/login') },
        { path: 'register', component: load('auth/register') }
      ]
    },

And the real pages with content:

    {
      path: '/',
      component: load('layouts/menu'),
      beforeEnter: checkAuth,
      children: [
        { path: 'profile', component: load('profile/profile'), meta: { title: 'Profile' } },
        { path: 'jokes', component: load('jokes/jokes'), meta: { title: 'Jokes' } }
      ]
    },

And at last a "File not found" page for everything undefined.

    { path: '*', component: load('error404') }

The mentioned _checkAuth()_ method will check if the user is already authenticated
through the authentication api module.

## Authentication module

This will be discussed later if it really is tested with a server.

It will contain methods to login, logout, register and to check the authentication.

# Themes

My next task was to go deeper into theming and optimize the login/register dialogs.

To get a common display I made a special layout which holds the common part and most of the styles:

    <template>
      <div>
        <q-toolbar color="secondary">
          <q-btn flat v-go-back=" '/' ">
            <q-icon name="arrow_back" />
          </q-btn>
          <q-toolbar-title>
            Alinex Admin Panel
            <div slot="subtitle">operation tasks easy and fast</div>
          </q-toolbar-title>
        </q-toolbar>

        <div class="input-page window-width bg-light column items-center no-wrap">
          <div class="input-card shadow-4 bg-white column items-center justify-center no-wrap">
            <router-view />
          </div>
        </div>
      </div>
    </template>

    <style lang="stylus">
      .input-card
        border-radius 5px
        margin-top -50px
        width 80vw
        max-width 600px
        margin 10vh
        .layout-padding
          margin 0 32px

      .submit
        >.q-btn
          margin 5px
    </style>

    <script>
      import { GoBack, QLayout, QToolbar, QBtn, QIcon, QToolbarTitle, QItemMain, QItem, QItemTile, QListHeader } from 'quasar'

      export default{
        data () {
          return {
            title: ''
          }
        },

        components: { QLayout, QToolbar, QBtn, QIcon, QToolbarTitle, QList, QSideLink, QItemSide, QItemMain, QItem, QItemTile, QListHeader },

        directives: { GoBack }
      }
    </script>

So the real pages could be shorter:

    <template>
      <div class="full-width">
        <q-toolbar color="secondary">
          <q-icon name="edit" />
          <q-toolbar-title>
            Login
          </q-toolbar-title>
        </q-toolbar>

        <div class="layout-view layout-padding">
          <q-field icon="mail" error-label="A valid email address is needed">
            <q-input v-model="credentials.email" placeholder="Your email address" @blur="$v.credentials.email.$touch" :error="$v.credentials.email.$error" class="full-width" ref="email" />
          </q-field>
          <q-field icon="vpn_key">
            <q-input v-model="credentials.password" type="password" placeholder="Your password" @blur="$v.credentials.password.$touch" :error="$v.credentials.password.$error" class="full-width" />
          </q-field>

          <div class="submit row reverse">
            <q-btn color="primary" @click="submit()">Login</q-btn>
            <q-btn color="secondary" v-go-back=" '/' ">Cancel</q-btn>
          </div>
        </div>
      </div>
    </template>

    <script>
      import { GoBack, QBtn, QToolbar, QIcon, QToolbarTitle, QField, QInput, Toast } from 'quasar'
      import { required, minLength, email } from 'vuelidate/lib/validators'
      import auth from '../../auth'

      export default {
        data () {
          return {
            credentials: {
              email: '',
              password: ''
            }
          }
        },

        mounted () {
          // on next Vue tick, to ensure
          // our Vue reference exists
          this.$nextTick(() => {
            // calling "next()" method:
            this.$refs.email.focus()
          })
        },

        validations: {
          credentials: {
            email: { required, email },
            password: { required, minLength: minLength(6) }
          }
        },

        methods: {
          submit () {
            this.$v.credentials.$touch()
            if (this.$v.credentials.$error) {
              Toast.create('Please review fields again.')
              console.log(this.$v.credentials.$error)
              return
            }
            auth.login(this.credentials, 'profile')
          }
        },

        components: { QBtn, QToolbar, QIcon, QToolbarTitle, QField, QInput },

        directives: { GoBack }
      }
    </script>

As you have seen I already added a lot other things like validation, error message
display on demand, autofocus...

<img src="/images/Screenshot_20180105_205316.png" class="img-responsive center-block" />


# Further steps

My next bigger steps will be to make the REST Server component and make connecting it with the frontend.


_Alexander Schilling_
