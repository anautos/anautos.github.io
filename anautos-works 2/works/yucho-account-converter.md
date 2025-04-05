---
layout: page
title: ゆうちょ口座→銀行振込用変換ツール
description: ゆうちょの記号-番号を銀行ネットバンク振込用口座情報に変換する無料ツール
permalink: /works/yucho-account-converter/
---

<h2>ゆうちょ振替口座 → 銀行ネットバンク変換ツール</h2>

<label for="jpNumber">ゆうちょ記号-番号（例: 00150-1-723128）:</label>
<input type="text" id="jpNumber" placeholder="例: 00150-1-723128" />
<button onclick="convert()">変換</button>
<div id="result"></div>

<script>
  function convert() {
    const input = document.getElementById('jpNumber').value.trim();
    const resultDiv = document.getElementById('result');
    const match = input.match(/^(\d{5})-(\d+)-?(\d+)?$/);
    if (!match) {
      resultDiv.innerHTML = "<p style='color:red;'>入力形式が正しくありません（例: 00150-1-723128）</p>";
      return;
    }
    const part1 = match[2];
    const part2 = match[3] || '';
    const number = (part1 + part2).padStart(8, '0');
    const account = number.slice(-7);
    resultDiv.innerHTML = `
      <table>
        <tr><th>項目</th><th>入力内容</th></tr>
        <tr><td>銀行名</td><td>ゆうちょ銀行</td></tr>
        <tr><td>金融機関コード</td><td>9900</td></tr>
        <tr><td>支店名（店番）</td><td>〇一九（019）</td></tr>
        <tr><td>預金種目</td><td>当座</td></tr>
        <tr><td>口座番号</td><td>${account}</td></tr>
      </table>
    `;
  }
</script>