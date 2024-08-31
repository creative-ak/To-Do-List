<template>
  <tbody>
    <tr>
      <th scope="row">{{item.id}}</th>
      <td>{{item.name}}</td>
      <td>{{(item.completed ==1)? 'Done':''}}</td>
      <td>
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
            class="mr-3"
            v-show="(item.completed ==1)? false:true"
        />
        <button class="btn-danger ml-3" @click="confirmDelete()">X</button>
      </td>
    </tr>
  </tbody>
</template>

<script>
export default {
    props: ["item"],
    methods: {
        updateCheck() {
            axios
                .put(`api/item/${this.item.id}`, {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios put", errors);
                });
        },
        removeItem() {
            axios
                .delete(`api/item/${this.item.id}`)
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios delte ", error);
                });
        },

        confirmDelete() {
          // Show a confirmation dialog
          if (confirm("Are you sure you want to delete this item?")) {
            this.removeItem();
          }
        }

    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: gray;
}
.item {
    word-break: break-all;
}
</style>
