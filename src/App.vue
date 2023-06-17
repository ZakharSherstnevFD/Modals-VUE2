<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="_container">
          <button @click="modalFirst = !modalFirst" class="btn btnPrimary">
            Show first modal
          </button>
          <button
            @click="modalSecond.show = !modalSecond.show"
            class="btn btnPrimary"
          >
            Show second modal
          </button>

          <TheModal
            @close="modalFirst = false"
            v-show="modalFirst"
            title="First modal"
          >
            <div slot="body">
              <p>
                Lorem ipsum dolor sit amet consectetur adipisicing elit.
                Dolorem, dolore.
              </p>
              <button class="btn btnPrimary" @click="modalFirst.show = false">
                close
              </button>
            </div>
          </TheModal>

          <TheModal
            @close="modalSecond.show = false"
            v-show="modalSecond.show"
            title="modal with form"
          >
            <div slot="body">
              <form @submit.prevent="submitSecondForm" action="">
                <label>name:</label>
                <input required v-model="modalSecond.name" type="text" />
                <label>e-mail:</label>
                <input required v-model="modalSecond.email" type="email" />
                <button class="btn btnPrimary">submit</button>
              </form>
            </div>
          </TheModal>

          <button
            @click="ModalValidate = !ModalValidate"
            class="btn btnPrimary"
          >
            Validate
          </button>
          <ModalValidate
            @close="ModalValidate = false"
            v-show="ModalValidate"
          ></ModalValidate>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import TheModal from "./components/TheModal.vue";
import ModalValidate from "./components/ModalValidate.vue";
export default {
  components: { TheModal, ModalValidate },
  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: "",
        email: "",
      },
      ModalValidate: false,
    };
  },
  methods: {
    submitSecondForm() {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email,
      });
      this.modalSecond.name = "";
      this.modalSecond.email = "";
      this.modalSecond.show = false;
    },
  },
};
</script>
