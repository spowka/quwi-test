<template>
  <div class="homeContainer">
    <div v-if="isLoggedIn">
      <div
        v-for="(item, index) in data"
        :key="index"
        class="card"
        @click="openModal(index, item.name)"
      >
        <img :src="item.logo_url" alt="logo" height="60px" />
        <p class="name">{{ item.name }}</p>
        <p v-if="item.is_active" class="active">Active</p>
        <p v-else class="disactive">Disactive</p>
        <table>
          <tbody>
            <tr>
              <td>time this week</td>
              <td>00:00:00</td>
            </tr>
            <tr>
              <td>his month</td>
              <td>00:00:00</td>
            </tr>
            <tr>
              <td>total</td>
              <td>00:00:00</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <div v-else class="notFound"><p>PAGE NOT FOUND</p></div>
    <Modal
      :name="current.name"
      @save="saveChange"
      @close="closeModal"
      v-show="isModalOpen"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoggedIn: false,
      data: [],
      isModalOpen: false,
      current: { name: "", index: "" },
    };
  },
  mounted() {
    this.isLoggedIn = !!localStorage.getItem("access_token");
    if (!!localStorage.getItem("access_token")) {
      this.$axios({
        url: "/projects-manage/index?filters[is_active]=1&sort=dta_create",
        method: "get",
        headers: {
          Authorization: `Bearer ${localStorage.getItem("access_token")}`,
        },
      })
        .then((res) => {
          console.log(res.data.projects);
          this.data = res.data.projects;
        })
        .catch(() => (this.isLoggedIn = false));
    }
  },
  methods: {
    openModal(index, name) {
      this.current = { index, name };
      this.isModalOpen = true;
      console.log(index);
    },
    saveChange(e) {
      console.log(e);
      this.isModalOpen = false;
      this.data[this.current.index].name = e;
    },
    closeModal() {
      console.log("close");
      this.isModalOpen = false;
    },
  },
};
</script>

<style scoped>
.notFound {
  width: 100%;
  height: calc(100vh - 85px);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 45px;
  font-weight: 600;
  color: rgb(51, 51, 51);
}
.homeContainer {
  width: 100%;
  min-height: calc(100vh - 45px);
  background: #efefef;
  padding: 20px 0;
  position: relative;
}
.card {
  width: 50%;
  margin: 0 auto;
  background: #fff;
  height: 100px;
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  cursor: pointer;
}
.card img {
  width: fit-content;
}
.card td {
  padding-right: 10px;
}
.name {
  width: 40%;
}
.active {
  width: 20%;
  color: rgb(33, 104, 33);
}
.disactive {
  width: 20%;
  color: rgb(104, 35, 33);
}
</style>
