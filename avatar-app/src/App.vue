<script>
const elements = ['air', 'earth', 'water', 'fire'];
export default {
  data:() => ({
    characterList: [
      {
        name: 'Aang',
        element: ['Air', 'Earth', 'Water', 'Fire']
      },
      {
        name: 'Zuko',
        element: ['Fire']
      },
      {
        name: 'Pilla',
        element: ['Earth']
      },
      {
        name: 'Gop',
        element: ['Water']
      },
    ],
    favoriteList: new Set(),
    newCharacter: {
      name: '',
      element: []
    }
  }),
  computed: {
    benderStatistics() {
      return elements.reduce((acc, curr) => {
        const stat = this.characterList.filter(character => character.element.find(el => el.toLowerCase() === curr)).length
        return { ...acc, [curr]: stat}
      }, {})
    }
  },
  methods: {
    addCharacterToFavorites(index) {
      this.favoriteList.add(this.characterList[index])
    },
    removeCharacterFromFavorites(index) {
      // this is not perfect because the indices of sets do not necessarily stay the same
      const array = Array.from(this.favoriteList)
      array.splice(index, 1)
      this.favoriteList = new Set(array)
    },
    addNewCharacter() {
      if (this.newCharacter.name && !this.characterList.find(c => c.name === this.newCharacter.name)) {
        this.characterList.push(this.newCharacter)
        this.newCharacter = {
          name: ''
        }
      }
    }
  }
}
</script>

<template>
  <h2>Statistics</h2>
  <ul>
    <li v-for="(stat, type, index) in benderStatistics" :key="`bender-${index}`">{{ type }}: {{ stat }}</li>
  </ul>
  <h2>Characters</h2>
  <label for="newCharacterInput">New Character</label>
  <input type="text" id="newCharacterInput" v-model="newCharacter.name" @keyup.enter="addNewCharacter">
  <button @click="addNewCharacter">Submit</button>
  <p v-if="!characterList.length">There are no characters</p>
  <ul>
    <li v-for="(character, index) in characterList" :key="`character-${index}`">
      <div>
        <p>{{character.name}}</p>
        <button @click="addCharacterToFavorites(index)" v-if="!favoriteList.has(characterList[index])">Add to favorites</button>
      </div>
    </li>
  </ul>
  <h3>Favorites</h3>
  <ul>
    <li v-for="(character, index) in favoriteList" :key="`favorite-${index}`">
      <div>
        <p>{{character.name}}</p>
        <button @click="removeCharacterFromFavorites(index)">Remove from favorites</button>
      </div>
    </li>
  </ul>
</template>

