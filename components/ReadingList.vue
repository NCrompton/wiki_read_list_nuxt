<template>
  <c-box class="">
    <c-box class="info-container" v-for="read in readlist" border-width="1px 0px 1px 0px">
      <c-grid template-columns="3fr 3fr 3fr 1fr">
        <div class="info-cell" @click="redirect(read.link)">{{ read.name }}</div>
        <div class="info-cell" @click="redirect(read.link)">{{ read.kind }}</div>
        <div class="info-cell">
          <c-input placeholder="Your Notes" />
        </div>
        <div class="info-cell icon-container">
          <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" fill="currentColor"
            class="bi bi-chevron-down cell-icon" viewBox="0 0 16 16">
            <path fill-rule="evenodd"
              d="M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z" />
          </svg>
        </div>
      </c-grid>
      <c-grid template-columns="6fr 4fr">
        <div></div>
        <c-box m="0px 0px 3px 3px">
          <c-tag>new</c-tag>
        </c-box>
      </c-grid>
    </c-box>
  </c-box>
</template>
<script lang="js">
export default {
  name: "ReadingList",
  props: {
    readlist: {
      type: Array,
    },
  },
  methods: {
    redirect(link) {
      window.open(link)
    }
  }
}
</script>
<style>
.info-cell {
  align-self: center;
  margin: 3px;
}

.info-container:hover {
  cursor: pointer;
  box-shadow: 0 0 5px #8f8;
  color: #585;
}

.info-link {
  text-decoration: none;
}

.icon-container {
  padding-left: 30px;
}

.cell-icon:hover {
  border: 1px solid;
  border-radius: 5px;
}
</style>
