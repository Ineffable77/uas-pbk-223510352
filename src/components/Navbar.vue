<!-- Navbar.vue -->
<template>
  <div class="q-pa-md q-gutter-sm flex-between aa ">
    <div class="left">
      <q-avatar class="profile">
        <q-icon name="account_circle" size="45px" />
      </q-avatar>
      <span class="profile-name">Randy Ivando</span>
    </div>
    <div class="right">
      <q-btn-dropdown
        flat
        label="Tugas Randy"
        color="blue-indigo-5"
        text-color="white"
        size="1rem"
        dense
      >
        <q-list style="min-width: 160px">
          <q-item v-for="task in tasks" :key="task.id" clickable v-ripple @click="openProject(task.url)">
            <q-item-section>{{ task.name }}</q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      tasks: [
        { id: 1, name: 'Tugas1', url: 'https://randy-project-cv.vercel.app' },
        { id: 2, name: 'Tugas2', url: 'https://tugas2-pbk-223510352.vercel.app' },
        { id: 3, name: 'Tugas3', url: 'https://tugas3-pbk-223510352.vercel.app' },
        { id: 4, name: 'Tugas4', url: 'https://tugas4-pbk-223510352.vercel.app/' },
        { id: 5, name: 'Tugas5', url: 'https://tugas5-pbk-223510352.vercel.app' },
        { id: 6, name: 'Tugas6', url: 'https://tugas6-pbk-223510352.vercel.app' },
        { id: 7, name: 'Tugas7', url: 'https://tugas7-pbk-223510352.vercel.app' },
      ],
    };
  },
  methods: {
    openProject(url) {
      window.open(url, '_blank');
    },
  },
};
</script>

<style>
.q-pa-md.q-gutter-sm.flex-between.aa {
  display: flex;
  justify-content: space-between;
  align-items: center;
}


.left {
  display: flex;
  align-items: center;
}

.profile-name {
  margin-left: 10px;
  color: white;
  font-size: 18px;
}

.right {
  display: flex;
  align-items: center;
}
</style>
