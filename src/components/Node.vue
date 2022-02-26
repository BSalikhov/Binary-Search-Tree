<template>
  <div class="node-group">
    <div class="node parent-node">
      {{ node.value }}
    </div>

    <div class="children-container">
      <div class="child-wrapper">
        <Node v-if="node.left" :node="node.left" />
      </div>

      <div class="child-wrapper">
        <Node v-if="node.right" :node="node.right" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    node: Object,
  },

  components: {
    Node: () => import("./Node.vue"),
  },
};
</script>

<style>
.parent-node {
  width: 100%;
  margin: 0 auto;
}

.children-container {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.node {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  font-size: 18px;
  font-weight: 600;
  border: 2px solid #555;
  border-radius: 100px;
}

.child-wrapper {
  width: 80px;
  height: 80px;
  display: flex;
  justify-content: center;
}
</style>
