---
title: Connecting Frontend and REST Server
layout: post
tags: NodeJS JavaScript Feathers REST Server Quasar Vuex
---

In my first steps I had to look over the possibilities. It's possible to directly call the REST Services, to use the feathers-client from own code or to integrate
the feathers client into the state management.

I decided to try both methods and use one of them or both.

# Server Connection

The configuration is done in feathers-client.js:

    import feathers, { authentication, socketio } from '@feathersjs/client'
    import io from 'socket.io-client'

    const socket = io('http://localhost:3030', {transports: ['websocket']})
    // on reconnection, reset the transports option, as the Websocket
    // connection may have failed (caused by proxy, firewall, browser, ...)
    socket.on('reconnect_attempt', () => {
      socket.io.opts.transports = ['polling', 'websocket']
    })

    const feathersClient = feathers()
      .configure(socketio(socket))
      .configure(authentication({ storage: window.localStorage }))

    export default feathersClient

This uses socket.io because it's a fast protocol and as fallback long running polling connection.

Now I can use this client config in Vue or Vuex store.

# Vue Integration

Using [vue-feathers](https://github.com/sunabozu/vue-feathers) the connection can easily be integrated directly into Vue so it is accessible in any component. The only changes in _main.js_ are:

    import vueFeathers from 'vue-feathers'
    import feathersClient from './feathers-client'

    Vue.use(vueFeathers, feathersClient)

Now in every component you get a new property called $services, which allows you to interact with all of your Feathers services. To subscribe on the events your services generate, you just need to use a separate feathers section in your component.

# State Management

To share state between components a central state management is the solution to
not do the changes multiple times for identical data.

In Vue this task can be done using [Vuex](https://vuex.vuejs.org/en/). The state of data together with it's changing methods id kept in a centralized tree which can be accessed from all components.

I first tested this with a simple counter app which should increment with each button click. I made a store:

    import Vue from 'vue'
    import Vuex from 'vuex'

    Vue.use(Vuex)

    const store = new Vuex.Store({
      state: { count: 0 },
      mutations: {
        increment (state) {
          state.count++
        }
      }
    })

    export default store

Now I only have to load and inject this store in my Vue instance:

    import Vue from 'vue'
    import Quasar, { Loading } from 'quasar'
    import router from './router'
    import store from './store'

    Vue.use(Quasar) // Install Quasar Framework

    Quasar.start(() => {
      new Vue({
        el: '#q-app',
        router,
        store,
        render: h => h(require('./App').default)
      })
    })

After that I can directly use it in any component:

    export default {
      methods: {
        goTo (link) {
          this.$store.commit('increment')
          console.log(this.$store.state.count) // -> 1...
          router.push(link)
        }
      }
    }

Definitions:
- State has the current value
- Getters are methods to access computed values from state
- Mutations are sync methods to change state
- Actions are async methods which call mutations later

With the _mapState_, _mapMutations_ and _mapActions_ helper the elements can be easily brought into the component.

# Store Integration

<img src="https://vuex.vuejs.org/en/images/vuex.png" class="img-responsive center-block" />

The Backend API here is the REST server based on feathers which like displayed above also has the ability to change data on it's own.

Therefore I added [feathers-vuex](https://github.com/feathers-plus/feathers-vuex)
with its two modules included:

1. The Service module adds a Vuex store for new services.
2. The Auth module sets up the Vuex store for authentication / logout.

In _store/index.js_:

    import feathersVuex from 'feathers-vuex'
    import feathersClient from '../feathers-client'

    const { service, auth } = feathersVuex(feathersClient, { idField: '_id' })

    const store = new Vuex.Store({
      strict: process.env.NODE_ENV !== 'production',
      plugins: [
        service('messages'),
        auth()
      ],
      ...
    })
    
# Further steps

The basic connection is established. My next step will be to integrate some services and authentication through this into the quasar client app to make the example complete.

_Alexander Schilling_
