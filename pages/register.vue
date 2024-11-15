<script setup>
const { $swal } = useNuxtApp();

// 表單格式
const userRegisteObject = ref({
  name: "",
  email: "",
  password: "",
  phone: "",
  birthday: "",
  address: {
    zipcode: "",
    detail: "",
  },
});

const sendContact = async () => {
  if (!userRegisteObject.value.name || !userRegisteObject.value.email || !userRegisteObject.value.password || !userRegisteObject.value.phone || !userRegisteObject.value.birthday || !userRegisteObject.value.address.zipcode || !userRegisteObject.value.address.detail) {
      $swal.fire({
        icon: "error",
        title: "所有欄位皆為必填",
        showConfirmButton: false,
        timer: 1500,
      });
      return;
    }

  const passwordPattern = /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$/;
  if (!passwordPattern.test(userRegisteObject.value.password)) {
    $swal.fire({
      icon: "error",
      title: "密碼需至少包含 8 碼，並英數混合",
      showConfirmButton: false,
      timer: 1500,
    });
    return;
  }

  const phonePattern = /^((\+886|0)?9\d{8}|(\+886|0)?\d{1,2}-\d{6,8})$/;
  if (!phonePattern.test(userRegisteObject.value.phone)) {
    $swal.fire({
      icon: "error",
      title: "電話格式錯誤",
      text: "請輸入正確的手機號碼或市內電話",
      showConfirmButton: false,
      timer: 1500,
    });
    return;
  }


  try {
    const response = await $fetch("https://todolist-api.hexschool.io/doc/#/%E4%BD%BF%E7%94%A8%E8%80%85/post_users_sign_up", {
      method: "POST",
      body: { ...userRegisteObject.value }, // 傳遞物件的值
    });
    $swal.fire({
      icon: "success",
      title: "恭喜您註冊成功",
      showConfirmButton: false,
      timer: 1500,
    });
  } catch (error) {
    $swal.fire({
      icon: "error",
      title: "註冊失敗",
      text: error.response?.data?.message || "請稍後再試",
      showConfirmButton: false,
      timer: 1500,
    });
  }
};

// 使用 sweetAlert2 套件顯示訊息
// $swal.fire({
//   position: "center",
//   icon: ...,
//   title: ...,
//   showConfirmButton: false,
//   timer: 1500,
// });
</script>

<template>
  <div class="bg-light py-3 py-md-5 vh-100">
    <div class="container">
      <div class="row justify-content-md-center">
        <div class="col-12 col-md-11 col-lg-8 col-xl-7 col-xxl-6">
          <div class="bg-white p-4 p-md-5 rounded shadow-sm">
            <h2 class="h3 mb-4">會員註冊</h2>
            <form @submit.prevent="sendContact">
              <div class="form-floating mb-4">
                <input
                  type="text"
                  class="form-control"
                  id="firstName"
                  placeholder="王小明"
                  v-model="userRegisteObject.name"
                  required
                />
                <label for="firstName"
                  >姓名 <span class="text-danger">*</span></label
                >
              </div>

              <div class="form-floating mb-4">
                <input
                  type="email"
                  class="form-control"
                  id="email"
                  placeholder="example@gmail.com"
                  pattern="^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
                  v-model="userRegisteObject.email"
                  required
                />
                <label for="email"
                  >信箱 <span class="text-danger">*</span></label
                >
              </div>

              <div class="form-floating mb-4">
                <input
                  type="password"
                  class="form-control"
                  id="password"
                  placeholder="請輸入 8 碼以上密碼，需包含英數"
                  pattern="^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$"
                  v-model="userRegisteObject.password"
                  required
                />
                <label for="password"
                  >密碼 <span class="text-danger">*</span></label
                >
              </div>

              <div class="form-floating mb-4">
                <input
                  type="tel"
                  class="form-control"
                  id="phone"
                  placeholder="0912345678 或 02-12345678"
                  pattern="^((\+886|0)?9\d{8}|(\+886|0)?\d{1,2}-\d{6,8})$"
                  v-model="userRegisteObject.phone"
                  required
                />
                <label for="phone">電話</label>
              </div>

              <div class="form-floating mb-4">
                <input
                  type="date"
                  class="form-control"
                  id="dateInput"
                  v-model="userRegisteObject.birthday"
                  required
                />
                <label for="dateInput">出生年月日</label>
              </div>

              <div class="row">
                <div class="col-md-6">
                  <div class="form-floating mb-4">
                    <input
                      type="text"
                      class="form-control"
                      id="zipcode"
                      placeholder="100"
                      pattern="\d{3,}"
                      v-model="userRegisteObject.address.zipcode"
                      required
                    />
                    <label for="zipcode">郵遞區號</label>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="form-floating mb-4">
                    <input
                      type="text"
                      class="form-control"
                      id="address"
                      placeholder="台北市中正區重慶南路一段"
                      v-model="userRegisteObject.address.detail"
                      required
                    />
                    <label for="address">詳細地址</label>
                  </div>
                </div>
              </div>

              <button class="btn btn-lg btn-primary w-100" type="submit">
                註冊
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
