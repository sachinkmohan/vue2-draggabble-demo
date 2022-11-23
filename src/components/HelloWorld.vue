<template>
  <main>
    <div class="mt-5 container">
      <div class="row justify-content-center border py-5">
        <div class="col-5">
          <h4 class="mb-3">Draggable 1</h4>
          <draggable class="draggable-list" :list="list1" group="my-group">
            <div class="list-item1x1" v-for="element in list1" :key="element.name">
              {{ element.name }}
            </div>
          </draggable>
        </div>

        <div id="button">
          <input type="text" id="widget" v-model="name">
          <button v-on:click="addWidgetItem">Add Widget Item</button>
        </div>
        <div class="col-5">
          <h4 class="mb-3">Draggable 2</h4>
          <draggable class="draggable-list" :list="list2" group="my-group">
            <div class="list-item2x2" v-for="element in sortedNames" :key="element.name">
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </main>
</template>
<script>
import draggable from "vuedraggable";
export default {
  components: {
    draggable,
  },
  data() {
    return {
      list1: [{ name: "Drag Me!" }],
      list2: [{ name: "Drag Me Too!"} , {name: "Drag 3"}],
      list3: [],
      name: "",
    };
  },
  methods: {
    addWidgetItem() {
      this.list2.push({name:this.name});
      console.log(this.list2.name)
    },
    sortArrayItems() {
      return [...this.list2].slice().sort(function(a,b) {
        return (a.name > b.name) ? 1 : -1;
      })
    }
  },
  // computed: {
  //   SortNames2() {
  //     return this.list2.sort((a,b) => a.name.localeCompare(b.name));
  //   }
  // }
  computed: {
      sortedNames: function(){
        function compare(a, b) {
          if(a.name < b.name)
            return -1;
          if(a.name > b.name)
            return 1;
          return 0;
        }
        return [...this.list2].sort(compare);
      }
    
  }
};
</script>
<style scoped>
.draggable-list {
  background: #3f51b5;
  color: #fff;
  border: 1px solid;
  height: 30vh;
}
.list-item1x1 {
  width: 50px;
  height: 50px;
  margin: 10px;
  padding: 40px;
  cursor: pointer;
  font-size: 18px;
  border-radius: 5px;
  background: #f44336;
  display: inline-block;
}
.list-item2x2 {
  margin: 10px;
  height: 100px;
  padding: 40px;
  cursor: pointer;
  font-size: 18px;
  border-radius: 5px;
  background: #f44336;
  display: inline-block;
}
</style>