<script setup>
import { data } from "../const/const";
const formatDate = (date) => {
  const options = { day: "numeric", month: "short" };
  return new Intl.DateTimeFormat("ru-RU", options).format(new Date(date));
};

const getStatus = (start, end) => {
  const currentDay = new Date();
  const startDay = new Date(start);
  const endDay = new Date(end);
  let message = "";
  let endsIn;
  if (startDay - currentDay < 0) {
    endsIn = Math.ceil((new Date(endDay) - new Date()) / (1000 * 60 * 60 * 24));
    if (endsIn > 2) {
      message = "Заканчивается через " + endsIn + " дней";
    } else if (endsIn == 1) {
      message = `Заканчивается завтра`;
    } else if (endsIn == 0) {
      message = `Заканчивается сегодня`;
    } else if (endsIn < 0) {
      message = "Закончилось " + Math.abs(endsIn) + " дней назад";
    }
  } else if (startDay - currentDay > 0) {
    endsIn = Math.ceil(
      (new Date(startDay) - new Date()) / (1000 * 60 * 60 * 24)
    );
    message = "Начинается через " + endsIn + " дней";
  }
  return message;
};
</script>
<template>
  <table class="table__container">
    <caption>
      Выгрузка данных из файла
    </caption>
    <thead class="table__thead">
      <tr class="table__tr">
        <th class="table__field table__field--sort" id="o_id">o_id</th>
        <th class="table__field table__field--sort" id="client_name">
          client_name
        </th>
        <th class="table__field table__field--sort" id="diets">diets</th>
        <th class="table__field table__field--sort" id="tariff">tariff</th>
        <th class="table__field table__field--sort" id="address">address</th>
        <th class="table__field table__field--sort" id="phone">phone</th>
        <th class="table__field table__field--sort" id="dates">dates</th>
        <th class="table__field table__field--sort" id="discount">discount</th>
        <th class="table__field table__field--sort" id="order_sum">
          order_sum
        </th>
        <th class="table__field table__field--sort" id="order_payed">
          order_payed
        </th>
        <th class="table__field table__field--sort" id="pay_status">
          pay_status
        </th>
        <th class="table__field table__field--sort" id="courier_comment">
          courier_comment
        </th>
        <th class="table__field table__field--sort" id="inner_comment">
          inner_comment
        </th>
        <th class="table__field table__field--sort" id="ends_in">ends in</th>
      </tr>
    </thead>
    <tbody class="table__tbody">
      <tr v-for="item in data" :key="item.o_id">
        <td>{{ item.o_id }}</td>
        <td class="client_name">{{ item.client_name }}</td>
        <td class="diets">
          <tr v-for="diet in item.diets" :key="diet">
            <td>{{ diet }}</td>
          </tr>
        </td>
        <td class="tariff">
          <tr v-for="(tarif, index) in item.tariff" :key="index">
            <td>{{ tarif }}</td>
          </tr>
        </td>
        <td>{{ item.address }}</td>
        <td>{{ item.phone }}</td>
        <td class="dates">
          <tr v-for="(date, index) in item.dates" :key="index">
            <td>
              {{ formatDate(date.start_date) }} -
              {{ formatDate(date.end_date) }}
            </td>
          </tr>
        </td>
        <td>{{ item.discount }}</td>
        <td>{{ item.order_sum }}</td>
        <td>{{ item.order_payed }}</td>
        <td>{{ item.pay_status }}</td>
        <td class="courier_comment">{{ item.courier_comment }}</td>
        <td class="inner_comment">{{ item.inner_comment }}</td>
        <td class="ends_in">
          <tr v-for="(date, index) in item.dates" :key="index">
            {{
              getStatus(date.start_date, date.end_date)
            }}
          </tr>
        </td>
      </tr>
    </tbody>
    <tfoot></tfoot>
  </table>
</template>

<style lang="scss" scoped>
.table__container {
  border: 1px solid #646cff;
  border-collapse: collapse;
}
.table__thead {
  cursor: pointer;
  height: 30px;
  color: white;
  background-color: #646cff;
}
.table__field {
  border: 1px solid rgb(175, 173, 173);
}
.table__tbody td {
  border: 1px solid #646cff;
}
.client_name {
  width: 70px;
}
.diets {
  & tr td {
    width: 100%;
    border: none;
    border-bottom: 1px solid gray;
  }
  & tr:last-child td {
    border: none;
  }
}
.tariff {
  width: 70px;
  & tr td {
    border: none;
    border-bottom: 1px solid gray;
  }
  & tr:last-child td {
    border: none;
  }
}
.dates,
.ends_in {
  width: 120px;
  & tr td {
    width: 100%;
    border: none;
    border-bottom: 1px solid gray;
  }
  & tr:last-child td {
    border: none;
  }
}
.inner_comment,
.courier_comment {
  width: 50px;
}
</style>
