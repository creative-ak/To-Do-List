<template>
    <div class="mt-4">
        <h4>List View</h4>
        <hr class="w-100 m-auto mb-3" />
        <!--<ul class="list-group m-auto"> -->
                    <table class="table table-bordered">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Task</th>
              <th scope="col">Status</th>
              <th scope="col">Action</th>
            </tr>
          </thead>

            <list-item
                :item="item"
                v-on:itemchanged="$emit('reloadlist')"
                v-for="item in items"
                :key="item.id"
                class="m-auto my-1 text-justify text-wrap"
            />
        <!--</ul> -->

        </table>
    </div>
</template>

<script>
import listItem from "./listItem";

export default {
    components: {
        listItem
    },
    props: ["items"]
};
</script>

<style scoped></style>
