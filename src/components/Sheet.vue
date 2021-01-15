<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-text-field solo label="Word" v-model="word"></v-text-field>
        <v-textarea
          solo
          label="Definition"
          v-model="definition"
          rows="4"
        ></v-textarea>

        <v-btn class="primary" @click="add()">
          Add
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-data-table
          :headers="headers"
          :items="items"
          :items-per-page="5"
          class="elevation-1"
        >
          <template v-slot:body="{ items }">
            <tbody>
              <tr v-for="(item, index) in items" :key="index">
                <td>{{ item.word }}</td>
                <td>{{ item.definition }}</td>
                <td>
                  <v-btn circle color="secondary" @click="edit(index)">
                    <v-icon>
                      mdi-pencil
                    </v-icon>
                  </v-btn>
                  <v-btn
                    class="ml-3"
                    circle
                    color="accent"
                    @click="remove(index)"
                  >
                    <v-icon>
                      mdi-trash-can
                    </v-icon>
                  </v-btn>
                </td>
              </tr>
            </tbody>
          </template>
        </v-data-table>
      </v-col>
    </v-row>
    <v-dialog v-model="dialog" max-width="290">
      <v-card>
        <v-card-title class="headline">
          Edit Item
        </v-card-title>

        <v-card-text>
          <v-text-field solo label="Word" v-model="word1"></v-text-field>
          <v-textarea
            solo
            label="Definition"
            v-model="definition1"
            rows="4"
          ></v-textarea>
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn color="green darken-1" text @click="update()">
            Save
          </v-btn>

          <v-btn color="green darken-1" text @click="dialog = false">
            Cancel
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
export default {
  name: 'Sheet',

  data: () => ({
    word: '',
    definition: '',
    word1: '',
    definition1: '',
    selectedIndex: 0,
    dialog: false,
    headers: [
      {
        text: 'Word',
        value: 'word',
      },
      { text: 'Definition', value: 'definition' },
      { text: 'Actions', value: '' },
    ],
    items: [],
  }),
  methods: {
    add() {
      if (this.word && this.definition) {
        this.items.push({ word: this.word, definition: this.definition });
        this.word = '';
        this.definition = '';
      }
    },
    edit(index) {
      this.selectedIndex = index;
      this.word1 = this.items[index].word;
      this.definition1 = this.items[index].definition;
      this.dialog = true;
    },
    update() {
      this.items[this.selectedIndex].word = this.word1;
      this.items[this.selectedIndex].definition = this.definition1;
      this.dialog = false;
    },
    remove(index) {
      this.items.splice(index, 1);
    },
  },
};
</script>
