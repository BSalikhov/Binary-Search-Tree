<template>
  <div id="app">
    <h1>Binary Search Tree</h1>

    <Form @add="add" @remove="remove" />

    <div v-if="tree.root && tree.root.value" class="tree-container">
      <NodeComponent :node="tree.root"> </NodeComponent>
    </div>
  </div>
</template>

<script>
import Form from "./components/Form.vue";
import NodeComponent from "./components/Node.vue";

class Node {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

class BST {
  constructor() {
    this.root = null;
  }

  add(value) {
    const node = this.root;
    if (node === null) {
      this.root = new Node(value);
      return;
    } else {
      const searchTree = function (node) {
        if (value < node.value) {
          if (node.left === null) {
            node.left = new Node(value);
            return;
          } else {
            searchTree(node.left);
          }
        } else if (value > node.value) {
          if (node.right === null) {
            node.right = new Node(value);
            return;
          } else {
            searchTree(node.right);
          }
        } else {
          return null;
        }
      };
      searchTree(node);
      return;
    }
  }

  remove(value) {
    const removeNode = function (node, value) {
      if (node == null) {
        return null;
      }
      if (value == node.value) {
        if (node.left == null && node.right == null) {
          return null;
        }

        if (node.right == null) {
          return node.left;
        }

        if (node.left == null) {
          return node.right;
        }

        var tempNode = node.right;
        while (tempNode.left !== null) {
          tempNode = tempNode.left;
        }
        node.value = tempNode.value;
        node.right = removeNode(node.right, tempNode.value);
        return node;
      } else if (value < node.value) {
        node.left = removeNode(node.left, value);
        return node;
      } else {
        node.right = removeNode(node.right, value);
        return node;
      }
    };
    this.root = removeNode(this.root, value);
  }
}

export default {
  name: "App",
  components: {
    Form,
    NodeComponent,
  },

  data: () => ({
    tree: new BST(),
  }),

  methods: {
    add(value) {
      this.tree.add(+value);
      console.log(value);
    },

    remove(value) {
      this.tree.remove(+value);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.tree-container {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 50px;
}
</style>
