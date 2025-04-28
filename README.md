<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Love Letter</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(to right, #ffdde1, #ee9ca7);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      text-align: center;
    }
    textarea {
      width: 300px;
      height: 150px;
      padding: 10px;
      border: 2px solid #fff;
      border-radius: 10px;
      margin-bottom: 10px;
      resize: none;
    }
    button {
      background-color: #ff6f91;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background-color: #ff4e70;
    }
    .link {
      margin-top: 20px;
      background: white;
      padding: 10px;
      border-radius: 10px;
      word-break: break-word;
      max-width: 80%;
    }
  </style>
</head>
<body>

  <h1>Write Your Love Letter 💌</h1>
  <textarea id="letter" placeholder="Write your love here..."></textarea><br>
  <button onclick="createLink()">Create Link</button>

  <div class="link" id="link" style="display:none;"></div>

  <script>
    function createLink() {
      const letter = encodeURIComponent(document.getElementById('letter').value);
      const url = window.location.origin + window.location.pathname + "?letter=" + letter;
      const linkDiv = document.getElementById('link');
      linkDiv.innerHTML = `<a href="${url}">${url}</a>`;
      linkDiv.style.display = "block";
    }

    window.onload = function() {
      const params = new URLSearchParams(window.location.search);
      const letter = params.get('letter');
      if (letter) {
        document.body.innerHTML = `
          <h1>Your Love Letter 💖</h1>
          <p style="white-space: pre-wrap; background: white; padding: 20px; border-radius: 10px; max-width: 600px;">${decodeURIComponent(letter)}</p>
        `;
      }
    }
  </script>

</body>
</html>

