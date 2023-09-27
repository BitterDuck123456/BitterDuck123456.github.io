<!DOCTYPE html>
<html>
<head>
  <title>凱薩密碼加密/解密</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    label {
      display: block;
    }
  </style>
</head>
<body>
  <h1>凱薩密碼加密/解密</h1>
  <label for="message">訊息：</label>
  <input type="text" id="message" placeholder="請輸入要加密/解密的訊息">
  <label for="shift">位移：</label>
  <input type="number" id="shift" placeholder="請輸入位移數字">
  <button onclick="encrypt()">加密</button>
  <button onclick="decrypt()">解密</button>
  <br>
  <label for="result">結果：</label>
  <input type="text" id="result" readonly>
  
  <script>
    function encrypt() {
      const message = document.getElementById("message").value;
      const shift = parseInt(document.getElementById("shift").value);
      const encryptedMessage = caesarCipher(message, shift);
      document.getElementById("result").value = encryptedMessage;
    }

    function decrypt() {
      const message = document.getElementById("message").value;
      const shift = parseInt(document.getElementById("shift").value);
      const decryptedMessage = caesarCipher(message, -shift); // 逆向位移以解密
      document.getElementById("result").value = decryptedMessage;
    }

    function caesarCipher(message, shift) {
      return message
        .split("")
        .map((char) => {
          if (char.match(/[a-zA-Z]/)) {
            const code = char.charCodeAt(0);
            const isUpperCase = char === char.toUpperCase();
            const base = isUpperCase ? 65 : 97;
            const encryptedCode = ((code - base + shift) % 26 + 26) % 26 + base;
            return String.fromCharCode(encryptedCode);
          }
          return char;
        })
        .join("");
    }
  </script>
</body>
</html>
