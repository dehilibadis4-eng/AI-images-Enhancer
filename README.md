<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>محسن الصور الذكي</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f2f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .wrapper {
      background: white;
      padding: 30px;
      border-radius: 12px;
      width: 380px;
      text-align: center;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }
    h2 {
      margin-bottom: 18px;
    }
    input[type="file"] {
      margin: 18px 0;
    }
    button {
      background: #007bff;
      color: white;
      border: none;
      padding: 10px 18px;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background: #0056b3;
    }
    #output {
      margin-top: 20px;
      max-width: 100%;
      border-radius: 8px;
    }
  </style>
</head>
<body>

<div class="wrapper">
  <h2>AI لتحسين جودة الصور</h2>
  <input type="file" id="inputImage" accept="image/*">
  <br>
  <button onclick="enhanceImage()">حسّن الصورة</button>
  <br>
  <img id="output" src="" alt="">
</div>

<script>
async function enhanceImage() {
  const input = document.getElementById("inputImage");
  const output = document.getElementById("output");

  if (!input.files || !input.files[0]) {
    alert("اختر صورة أولاً!");
    return;
  }

  const file = input.files[0];
  const formData = new FormData();
  formData.append("image", file);

  // مفتاح API مجاني من DeepAI (يمكنك تغييره لاحقًا)
  const API_KEY = "quickstart-QUdJIGlzIGNvbWluZy4uLi4K";
  const response = await fetch("https://api.deepai.org/api/torch-srgan", {
    method: "POST",
    body: formData,
    headers: {
      "Api-Key": API_KEY
    }
  });

  const data = await response.json();
  if (data.output_url) {
    output.src = data.output_url;
  } else {
    alert("حدث خطأ أثناء تحسين الصورة!");
  }
}
</script>

</body>
</html>

