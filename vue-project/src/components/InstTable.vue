<template>
  <div class="container">
    <!-- ヘッダー -->
    <div class="header flex justify-between items-center mb-4">
      <h2 class="text-xl font-bold">インスト管理アプリ</h2>
      <button 
        v-if="activeIndex !== null"
        @click="goBack" 
        class="bg-gray-500 text-white px-4 py-2 rounded-full">
        トップページに戻る
      </button>
    </div>

    <!-- 詳細表示用 -->
    <div v-if="activeIndex !== null">
      <p class="mb-4">詳細: {{ items[activeIndex].detail }}</p>

      <!-- メモ欄 -->
      <textarea
        v-model="memo"
        placeholder="メモを入力..."
        class="w-full h-24 border rounded p-2 mb-4"
      ></textarea>

      <button 
        class="bg-blue-500 text-white px-4 py-2 rounded-full" 
        @click="nextStep">
        次へ
      </button>
    </div>

    <!-- 項目一覧 -->
    <table v-if="activeIndex === null" class="table-auto w-full border-collapse border border-gray-300">
      <thead>
        <tr class="bg-gray-200">
          <th class="border px-4 py-2">項目</th>
          <th class="border px-4 py-2">詳細</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="index" class="cursor-pointer hover:bg-gray-100">
          <td class="border px-4 py-2">
            <button @click="viewDetail(index)" class="bg-green-500 text-white px-4 py-2 rounded">
              {{ item.name }}
            </button>
          </td>
          <td class="border px-4 py-2">{{ item.detail }}</td>
        </tr>
      </tbody>
    </table>

    <!-- 最後のメッセージ -->
    <div v-if="isEnd" class="mt-4 text-xl font-bold text-green-500">
      インスト終わりです！お疲れ様！
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { name: "項目1", detail: "項目1の詳細です" },
        { name: "項目2", detail: "項目2の詳細です" },
        { name: "項目3", detail: "項目3の詳細です" },
      ],
      activeIndex: null,  // 詳細表示用の項目インデックス
      isEnd: false,  // インストが終わったかどうか
      memo: "", // メモを保存する変数
    };
  },
  methods: {
    // 項目の詳細を表示
    viewDetail(index) {
      this.activeIndex = index;
    },
    // 次の項目に進む
    nextStep() {
      if (this.activeIndex < this.items.length - 1) {
        this.activeIndex++;
      } else {
        this.isEnd = true;  // 最後の項目に到達したら「インスト終わりです！」を表示
      }
    },
    // トップページに戻る
    goBack() {
      this.activeIndex = null;  // 項目一覧に戻る
      this.memo = ""; // メモ欄をリセット
    },
  },
};
</script>

<style>
.container {
  padding: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 10px;
  text-align: left;
}

button {
  cursor: pointer;
}

button:focus {
  outline: none;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}
</style>
