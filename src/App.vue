<script setup>
import { reactive } from "vue";

const data = reactive({
  sender: "",
  billTo: "",
  shipTo: "",
  invoice: "",
  date: "",
  DueDate: "",
  AdditionalNote: "",
  items: [
    {
      description: "",
      quantity: "",
      rate: "",
      amount: "",
    },
  ],
  description: "",
  quantity: "",
  rate: "",
  notes: "",
  terms: "",
  tax: "",
});

function addMoreItems() {
  data.items.push({
    description: "",
    quantity: "",
    rate: "",
    amount: "",
  });
  const getSubTotal = () => {
    let subtotal = 0;
    data.items.forEach((item) => {
      subtotal += item.amount;
    });
    data.subtotal = subtotal;
    return subtotal;
  };
}
</script>

<template>
  <section
    class="container min-h-screen p-12 mx-auto bg-white border border-gray-400"
  >
    <div class="flex justify-between">
      <div class="flex flex-col space-y-5 w-1/2s">
        <div class="">
          <img
            class="w-40"
            src="https://www.shutterstock.com/image-vector/invoice-typographic-stamp-sign-badge-600w-1027820257.jpg"
            alt=""
          />
        </div>
        <p class="mt-5">Sender</p>
        <textarea
          name=""
          id=""
          cols="30"
          rows="2"
          v-model="data.sender"
        ></textarea>
        <div class="flex space-x-2">
          <div class="flex flex-col">
            <span>Bill to</span>
            <textarea
              name=""
              id=""
              cols="30"
              rows="2"
              v-model="data.billTo"
            ></textarea>
          </div>
          <div class="flex flex-col">
            <span>Ship to</span>
            <textarea
              name=""
              id=""
              cols="30"
              rows="2"
              v-model="data.shipTo"
            ></textarea>
          </div>
        </div>
      </div>
      <div class="flex flex-col items-end w-1/2">
        <h1 class="mt-12 mb-5 text-4xl text-right uppercase">Invoice</h1>
        <input
          class="w-[200px] text-right"
          type="text"
          placeholder="Invoice Number"
          v-model="data.invoice"
        />
        <div class="w-full mt-10 space-y-3 text-right flex-y-5">
          <p>
            <span>Date</span>
            <input class="ml-2 w-[200px]" v-model="data.date" />
          </p>
          <p>
            <span>Due Date</span>
            <input type="date" class="ml-2 w-[200px]" v-model="data.DueDate" />
          </p>
          <p>
            <span>Additional Note</span>
            <input
              class="ml-2 w-[200px]"
              type="text"
              v-model="data.AdditionalNote"
            />
          </p>
        </div>
      </div>
    </div>
    <div class="mt-20">
      <table class="w-full table-auto">
        <tr class="text-left text-white bg-gray-800">
          <th class="w-1/2 p-2 pl-5">Item</th>
          <th class="p-2">Quantity</th>
          <th class="p-2">Rate</th>
          <th class="p-2 w-[200px] text-right pr-5">Amount</th>
        </tr>
        <tr v-for="(item, index) in data.items" :key="index">
          <td class="py-1">
            <input
              class="w-full pl-5"
              type="text"
              placeholder="Description"
              v-model="item.description"
            />
          </td>
          <td class="">
            <input
              class="w-full"
              type="number"
              placeholder="Quantity"
              v-model="item.quantity"
            />
          </td>
          <td class="">
            <input
              class="w-full"
              type="number"
              placeholder="Rate"
              v-model="item.rate"
            />
          </td>
          <td class="py-1 pr-5 text-right text-gray-800">
            {{ (item.amount = item.quantity * item.rate) }}
          </td>
        </tr>
      </table>

      <button
        @click="addMoreItems()"
        class="px-4 py-2 mt-5 font-bold text-white bg-green-600 rounded hover:bg-green-700"
      >
        Add More
      </button>
      <button
        class="px-4 py-2 mt-5 ml-5 font-bold text-white bg-green-600 rounded hover:bg-green-700"
      >
        Load Invoice #1
      </button>
      <button
        class="px-4 py-2 mt-5 ml-5 font-bold text-white bg-green-600 rounded hover:bg-green-700"
      >
        Load Invoice #2
      </button>
      <p class="mt-10">
        {{ data }}
      </p>
    </div>
    <div class="mt-[200px]">
      <div class="flex justify-between">
        <div class="flex flex-col w-1/2 space-y-5">
          <span>Notes</span>
          <textarea
            name=""
            id=""
            cols="30"
            rows="2"
            v-model="data.notes"
          ></textarea>
          <span>Terms</span>
          <textarea
            name=""
            id=""
            cols="30"
            rows="2"
            v-model="data.terms"
          ></textarea>
        </div>
        <div class="flex flex-col items-end w-1/2">
          <div class="w-full mt-10 space-y-3 text-right flex-y-5">
            <p>
              <span>Subtotal</span>
              <input
                @click="getSubTotal()"
                readonly
                class="focus:ring-0 focus:ring-offset-0 text-right ml-2 pr-4 w-[200px] border-0"
                placeholder="Subtotal"
              />
            </p>
            <p>
              <span>Tax</span>
              <input
                type="number"
                class="text-right w-[200px] ml-2"
                v-model="data.tax"
              />
            </p>
            <p>
              <span>Total</span>
              <input
                readonly
                class="focus:ring-0 focus:ring-offset-0 text-right ml-2 pr-4 w-[200px] border-0"
                placeholder="Total"
              />
            </p>
            <p>
              <span>Balance Due</span>
              <input
                readonly
                class="focus:ring-0 focus:ring-offset-0 text-right ml-2 pr-4 w-[200px] border-0"
                placeholder="Balance"
              />
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
input,
textarea {
  border: 1px solid #ddd !important;
  padding: 5px;
}
</style>
