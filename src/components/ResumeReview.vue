<template>
  <v-dialog
  v-model="dialog"
  fullscreen
  hide-overlay
  transition="dialog-bottom-transition">
    <v-card>
      <v-card-title class="headline">
          <v-row>
            <v-col cols="12" sm="11">
            <v-avatar class="ma-2">
              <img
                :src="person.img"
              >
            </v-avatar>
              <span v-html="person.name"></span>
            </v-col>
            <v-col cols="12" sm="1" align-self="end" class="d-flex justify-end">
              <v-btn text icon color="dark" @click="dialog = false">
                <v-icon>close</v-icon>
              </v-btn>
            </v-col>
          </v-row>
      </v-card-title>
      <v-card-text>Let Google help apps determine location.</v-card-text>
      <v-card-actions>
        <form @submit="saveForm" class="resume-review__form">
          <v-container fluid>
            <v-row>
              <v-col cols="12">
                <v-expansion-panels accordion>
                    <v-expansion-panel
                      v-for="(item,i) in formData"
                      :key="i"
                    >
                    <v-expansion-panel-header>
                      <span class="text-left">{{i === 1 ? 'Hard Skills' : 'Soft skills'}}</span>
                    </v-expansion-panel-header>
                    <v-expansion-panel-content>
                      <v-container fluid>
                        <v-row v-for="(subItem, subItemKey) in item" :key="subItemKey + 'raiting'">
                          <v-col cols="12" sm="6">
                            {{subItem.text}}
                          </v-col>
                          <v-col cols="12" sm="5">
                            <div class="text-center">
                              <v-rating v-model="subItem.raiting"></v-rating>
                            </div>
                          </v-col>
                          <v-col cols="12" sm="1">
                            <v-btn text medium
                            @click="toggleNote(i, subItemKey, subItem.makeNote)">+ Note</v-btn>
                          </v-col>
                          <v-col cols="12">
                            <v-textarea
                              transition="dialog-bottom-transition"
                              v-show="subItem.makeNote"
                              filled
                              name="input-7-4"
                              label="Skill note"
                              v-model="subItem.note"
                            ></v-textarea>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-expansion-panel-content>
                  </v-expansion-panel>
                </v-expansion-panels>
              </v-col>
              <v-col cols="12">
                <v-btn small color="primary" type="submit">Save</v-btn>

                <v-btn small color="error" class="ml-2"
                 type="reset" @click="resetForm">Reset</v-btn>
              </v-col>
            </v-row>

          </v-container>
        </form>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {

  props: {
    person: {
      type: Object,
      default() {
        return {
          name: 'SayMay',
          img: 'https://cdn.vuetifyjs.com/images/lists/1.jpg',
        };
      },
    },

    showDialog: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      dialog: false,
      item: 1,
      buttonValue: false,

      items: [
        {
          title: 'Skills',
          subtitle: "<span class='text--primary'>Ali Connors</span> &mdash; I'll be in your neighborhood doing errands this weekend. Do you want to hang out?",
          items: [
            {
              rating: 0,
              text: 'some random text',
            },
          ],
        },
      ],

      formData: [
        [
          {
            rating: 0,
            note: '',
            text: 'Ability to think on your feet',
          },
          {
            rating: 0,
            note: '',
            text: 'Commutication',
          },
          {
            rating: 0,
            note: '',
            text: 'Management',
          },
        ],
        [
          {
            rating: 0,
            note: '',
            text: 'html',
          },
          {
            rating: 0,
            note: '',
            text: 'css',
          },
          {
            rating: 0,
            note: '',
            text: 'js',
          },
        ],
      ],
    };
  },

  watch: {
    showDialog(newVal) {
      this.dialog = newVal;
    },

    dialog(newVal) {
      if (!newVal) {
        this.resetForm();
      }
      this.$emit('update:showDialog', newVal);
    },
  },

  methods: {
    addToggleNoteToForm() {
      this.formData = this.formData.map(item => item.map(value => ({ ...value, makeNote: false })));
    },

    saveForm(e) {
      e.preventDefault();
    },

    resetForm() {
      this.formData = this.formData.map(item => item.map(value => ({
        ...value, raiting: 0, note: '', makeNote: false,
      })));
    },

    toggleNote(fromSectionKey, formItemKey, showNote) {
      const isShowNote = !showNote;
      this.formData[fromSectionKey][formItemKey].makeNote = isShowNote;
      this.formData = this.formData;
    },
  },

  mounted() {
    this.addToggleNoteToForm();
  },
};
</script>

<style lang="scss">
.resume-review {
  &__form {
    width: 100%;
  }
}
</style>
