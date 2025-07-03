# Aminehh.github
Meio
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Amine - معرض الصور والفيديو</title>
<style>
  body {
    background-color: #121212;
    color: white;
    font-family: Arial, sans-serif;
    margin: 20px;
  }
  #gallery {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  .media-item {
    width: 200px;
    max-height: 150px;
    overflow: hidden;
    border: 2px solid #444;
    border-radius: 8px;
  }
  .media-item img, .media-item video {
    width: 100%;
    height: auto;
    display: block;
  }
  #uploadSection {
    margin-bottom: 20px;
  }
  #uploadBtn {
    padding: 10px 20px;
    background-color: #007bff;
    border: none;
    color: white;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
  }
  #uploadBtn:disabled {
    background-color: #555;
    cursor: not-allowed;
  }
</style>
</head>
<body>

<h1>معرض الصور والفيديو - Amine</h1>

<div id="uploadSection">
  <button id="uploadBtn">رفع ملفات</button>
  <input type="file" id="fileInput" multiple accept="image/*,video/*" style="display:none" />
</div>

<div id="gallery"></div>

<script>
  const uploadBtn = document.getElementById('uploadBtn');
  const fileInput = document.getElementById('fileInput');
  const gallery = document.getElementById('gallery');

  const PASSWORD = '1234'; // غير كلمة المرور هنا

  // عند الضغط على زر الرفع، نسأل عن كلمة المرور
  uploadBtn.addEventListener('click', () => {
    const pass = prompt('من فضلك أدخل كلمة المرور للرفع:');
    if (pass === PASSWORD) {
      fileInput.click();
    } else {
      alert('كلمة المرور خاطئة!');
    }
  });

  fileInput.addEventListener('change', (event) => {
    const files = event.target.files;

    for (let i = 0; i < files.length; i++) {
      const file = files[i];
      const url = URL.createObjectURL(file);

      const div = document.createElement('div');
      div.className = 'media-item';

      if (file.type.startsWith('image/')) {
        const img = document.createElement('img');
        img.src = url;
        div.appendChild(img);
      } else if (file.type.startsWith('video/')) {
        const video = document.createElement('video');
        video.src = url;
        video.controls = true;
        div.appendChild(video);
      }

      gallery.appendChild(div);
    }

    // إعادة تعيين الاختيار حتى نتمكن من رفع نفس الملفات مرة أخرى
    fileInput.value = '';
  });
</script>

</body>
</html>
