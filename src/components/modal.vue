<template>
  <div class="modal" @click.self="closeModal">
    <div class="modal-body">
      <div class="modal-body__remove" @click.self="closeModal"></div>
      <h2 class="modal-body__title">Add Social Profile</h2>
      <div class="modal-body__text">Add new social profile for tracking</div>
      <form class="modal-form" @submit.prevent="addSocial">
        <label for="url" class="modal-form__label">url</label>
        <input
          id="url"
          type="text"
          class="modal-form__input"
          :class="{ 'modal-form__input--invalid': error }"
          placeholder="https://twitter.com/username"
          v-model="url"
        />
        <button
          type="submit"
          class="modal-form__submit"
          :disabled="url.length < 6"
        >
          loolup
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "",
      error: false,
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
    addSocial() {
      const result = this.url.replace(/https:\/\//, "").match(/\w+(|-)\w+/);
      this.$emit("getUrl", result[0]);
      this.closeModal();
    },
  },
};
</script>

<style lang="scss" scoped>
.modal {
  position: fixed;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 999;
}
.modal-body {
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  padding: 25px;
  width: 600px;
  box-sizing: border-box;
  background-color: #fff;
  color: #4f4f4f;

  @media screen and (max-width: 767px) {
    width: 500px;
  }
  @media screen and (max-width: 575px) {
    width: 100%;
  }
  &__remove {
    position: absolute;
    top: 25px;
    right: 25px;
    width: 15px;
    height: 15px;
    cursor: pointer;

    &::before,
    &::after {
      content: "";
      position: absolute;
      top: 50%;
      left: 50%;
      width: 15px;
      height: 2px;
      background-color: #4f4f4f;
    }
    &::before {
      transform: translate(-50%, -50%) rotate(45deg);
    }
    &::after {
      transform: translate(-50%, -50%) rotate(-45deg);
    }
  }
  &__title {
    font-size: 18px;
    font-weight: 700;
    color: inherit;
    margin-bottom: 30px;
  }
  &__text {
    font-size: 14px;
    color: inherit;
    line-height: 17px;
    margin-bottom: 19px;
  }
}
.modal-form {
  display: flex;
  flex-direction: column;
  color: inherit;

  &__label {
    display: block;
    font-size: 13px;
    font-weight: 700;
    color: inherit;
    text-transform: uppercase;
    margin-bottom: 8px;
  }
  &__input {
    font-size: 14px;
    line-height: 16px;
    color: inherit;
    background-color: #fff;
    border: 1px solid #c5cfc9;
    border-radius: 6px;
    padding: 11px 22px 11px 16px;
    margin-bottom: 20px;

    &::placeholder {
      opacity: 0.7;
    }
    &::-moz-placeholder {
      opacity: 0.7;
    }
    &:-ms-input-placeholder {
      opacity: 0.7;
    }
    &::-webkit-input-placeholder {
      opacity: 0.7;
    }
    &--invalid {
      border-color: red;
    }
  }
  &__submit {
    align-self: flex-end;
    display: block;
    font-family: inherit;
    font-size: 14px;
    line-height: 38px;
    color: #fff;
    text-transform: capitalize;
    background: linear-gradient(180deg, #53cd72 0%, #1caf5e 100%);
    border-radius: 6px;
    border: none;
    width: 117px;
    box-sizing: border-box;
    outline: none;
    cursor: pointer;

    &:hover,
    &:focus {
      background: #1caf5e;
    }
    &:disabled {
      background: #ccc;
      cursor: default;
    }
  }
}
</style>