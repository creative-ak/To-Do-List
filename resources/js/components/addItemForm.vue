<template>
    <div class="mt-3">
        <!-- <h2>Add item form</h2> -->
        <div class="container m-2 w-100">
            <input
                type="test"
                placeholder="Add item"
                class="border"
                v-model="item.name"
            />
            <button
                :class="[item.name ? 'active' : 'notactive']"
                @click="addItem()"
            >
                Add +
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        };
    },
    methods: {
        addItem() {
            if (this.item.name == "") {
                return;
            }

            axios
                .post("api/item/store", {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 201) {
                        this.item.name = "";
                        this.$emit("reloadlist");
                    }else{
                        console.log(res.data.error);
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    }
};
</script>

<style scoped>
.active {
    color: white;
    background-color: blue;
}
.inactive {
    color: gray;
}
</style>
