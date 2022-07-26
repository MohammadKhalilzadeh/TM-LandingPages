<template>
  <div class="getstart">
    <center>
    <div id="head">
      <h2>
        {{ $t("GetStart_title") }}
      </h2>
    </div>

    <div id="reg-form">
      <div class="row row-cols-auto">
        <div class="col">
          <input
            type="text"
            class="form-control"
            aria-label="Sizing example input"
            aria-describedby="inputGroup-sizing-default"
            v-bind:placeholder="$t('GetStart_field1')"
            v-model="firstname"
          />
        </div>
        <div class="col">
          <input
            type="text"
            class="form-control"
            aria-label="Sizing example input"
            aria-describedby="inputGroup-sizing-default"
            v-bind:placeholder="$t('GetStart_field2')"
            v-model="lastname"
          />
        </div>
        <div class="col">
          <input
            type="text"
            class="form-control"
            aria-label="Sizing example input"
            aria-describedby="inputGroup-sizing-default"
            v-bind:placeholder="$t('GetStart_field3')"
            v-model="email"
          />
        </div>
        <div class="col">
          <input
            type="text"
            class="form-control"
            aria-label="Sizing example input"
            aria-describedby="inputGroup-sizing-default"
            v-bind:placeholder="$t('GetStart_field4')"
            v-model="phone"
          />
        </div>
        <div class="col">
          <input
            type="password"
            class="form-control"
            aria-label="Sizing example input"
            aria-describedby="inputGroup-sizing-default"
            v-bind:placeholder="$t('GetStart_field5')"
            v-model="password" />
        </div>
        <div class="col">
          <input
            type="password"
            class="form-control"
            aria-label="Sizing example input"
            aria-describedby="inputGroup-sizing-default"
            v-bind:placeholder="$t('GetStart_field6')"
            v-model="repassword"
          />
        </div>
      </div>
      <br>
      <center>
        <button v-on:click="regisrter">
          {{ $t("GetStart_Btn") }}
        </button>
      </center>
    </div>
    </center>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    msg: String,
  },
  data() {
    return {
      firstname: "",
      lastname: "",
      email: "",
      phone: null,
      password: "",
      repassword: "",
    };
  },
  methods: {
    regisrter: function () {
      if (this.password == this.repassword) {
        axios
          .post(process.env.VUE_APP_API_URL + "users", {
            firstname: this.firstname,
            lastname: this.lastname,
            email: this.email,
            password: this.password,
            phone: this.phone,
          })
          .then((response) => {
            if (response.status == 201) {
              this.firstname = "";
              this.lastname = "";
              this.email = "";
              this.password = "";
              this.repassword = "";
              this.phone = null;
              window.location.reload();
              this.$router.push({
                name: "Login",
              });
              alert(" خوش آمدید، حساب کاربری شما ایجاد شد حال وارد شوید ");
            } else if (response.status == 409) {
              alert(
                "متاسفانه این مشخصات از پیش توسط کاربران دیگر استفاده شده است"
              );
            } else if (response.status == 503) {
              alert(" در حال حاضر سیستم قادر به ارائه خدمات نیست ");
            } else {
              alert(" مشکل غیر منتظره، لطفا پس از مدتی دوباره امتحان کنید. ");
            }
          });
      } else {
        alert("مقدار فیلدهای پسورد نباید متفاوت باشد");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.getstart {
  color: white;
  background: url("../assets/header4.webp") ;
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  box-shadow: 8px 8px 8px 8px rgba(0, 0, 0, 0.2),
    8px 8px 20px 8px rgba(0, 0, 0, 0.19);
    min-height: 80vh;
}

#head {
  width: 100%;
  padding: 1%;
  background-color: #26262694;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

#reg-form{
  width: 90%;
  margin: 5%;
  padding: 2%;
  text-align: justify;
  align-content: center;
  color: #fff;
  background: #262626af;
  border-radius: 30px;
    box-shadow: 0 4px 8px 0 rgba(17, 17, 17, 0.529), 0 6px 20px 0 rgba(17, 17, 17, 0.529);
}

.row {
  width: 90%;
  margin: 1% 5%;
}

button {
  border: 1px solid white;
  color: white;
  background: #26262683 ;
  padding: 10px 40px;
  text-decoration: none;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 20px;
}

button:hover {
  border:1px solid #26262683 ;
  background: white;
  color: #26262683 ;
}

input {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  width: 90%;
  border-radius: 8px;
}

@media screen and (min-width: 320px) {
  .col {
    width: 100%;
    padding: 2%;
  }
}

@media screen and (min-width: 500px) {
  .col {
    width: 100%;
    padding: 1%;
  }
}


@media screen and (min-width: 900px) {
  .col {
    width: 50%;
    padding: 1%;
  }
}
</style>
