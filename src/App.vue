<template>
  <div id="app">
    <v-app id="inspire">
      <v-navigation-drawer
          v-model="isDrawerOpen"
          app
      >
        <v-list>
          <v-list-item link>
            <v-list-item-action>
              <v-icon>mdi-home</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>Home</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item link>
            <v-list-item-action>
              <v-icon>mdi-email</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>Contact</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>



      <v-app-bar
          app
          dark
          src="../public/bg.jpg"
          color="light-blue darken-2"
          extension-height="100px"
          hide-on-scroll
          >

        <v-app-bar-nav-icon @click.stop="isDrawerOpen = !isDrawerOpen"></v-app-bar-nav-icon>
        <v-toolbar-title>CJ TodoList</v-toolbar-title>


        <v-spacer></v-spacer>
        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <template v-slot:extension>
          <v-text-field
              v-model="newEventName"
              label="What to do next ?"
              solo
              light
              hide-details="auto"
              append-icon="mdi-plus"
              @click:append="addEvent"
              @keydown.enter="addEvent"
              :error-messages="errTips"
          ></v-text-field>
        </template>

      </v-app-bar>


      <v-container fluid>
        <v-content>

          <v-container>
            <v-row justify="center" align="center">
              <v-col cols="12">

              </v-col>
            </v-row>
          </v-container>

          <v-row justify="center">
            <v-col cols="12">
              <v-list>

                <v-slide-y-transition
                    group
                    tag="v-list-item"
                    class="py-0"
                >
                  <v-list-item
                      v-for="todoItem in todoItems"
                      :key="todoItem.id"
                  >
                    <v-list-item-action>
                      <v-checkbox
                          v-model="todoItem.isDone"
                      ></v-checkbox>
                    </v-list-item-action>
                    <v-list-item-content
                        :class="todoItem.isDone ? 'text-decoration-line-through text--disabled' : ''"
                    >{{ todoItem.eventName }}
                    </v-list-item-content>
                  </v-list-item>
                </v-slide-y-transition>
              </v-list>

            </v-col>
          </v-row>


        </v-content>
      </v-container>
    </v-app>
  </div>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    isDrawerOpen: false,
    newEventName: '',
    errTips: '',
    todoItems: [
      {
        id: 1,
        isDone: false,
        eventName: 'I am an event'
      }
    ]
  }),

  methods: {
    addEvent() {
      let f_this = this;
      if (this.newEventName === '') {

      } else {
        let newId = this.todoItems.length + 1;
        this.todoItems.push(
            {
              id: newId,
              isDone: false,
              eventName: this.newEventName
            }
        );
        this.errTips = '';
      }

    }
  }
};
</script>
