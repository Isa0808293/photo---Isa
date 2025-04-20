<!DOCTYPE html><html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Моя Фото-Галерея</title>
  <style>
    body {
      font-family: sans-serif;
      background-color: #f0f0f0;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #333;
    }
    .gallery {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: center;
      margin-top: 20px;
    }
    .gallery img {
      max-width: 200px;
      max-height: 200px;
      object-fit: cover;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    .upload-form {
      margin-top: 20px;
    }
    .upload-form input[type="file"] {
      margin-bottom: 10px;
    }
    .upload-form button {
      background-color: #4CAF50;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Моя Фото-Галерея</h1>  <form class="upload-form" id="uploadForm">
    <input type="file" name="photo" accept="image/*" required>
    <br>
    <button type="submit">Загрузить фото</button>
  </form>  <div class="gallery" id="gallery"></div>  <script>
    const form = document.getElementById('uploadForm');
    const gallery = document.getElementById('gallery');

    const SERVER_URL = 'https://ТВОЙ-СЕРВЕР.onrender.com'; // ЗАМЕНИ на свой

    async function loadPhotos() {
      const res = await fetch(`${SERVER_URL}/photos`);
      const urls = await res.json();
      gallery.innerHTML = '';
      urls.forEach(url => {
        const img = document.createElement('img');
        img.src = SERVER_URL + url;
        gallery.appendChild(img);
      });
    }

    form.addEventListener('submit', async (e) => {
      e.preventDefault();
      const formData = new FormData(form);
      await fetch(`${SERVER_URL}/upload`, {
        method: 'POST',
        body: formData
      });
      form.reset();
      loadPhotos();
    });

    loadPhotos();
  </script></body>
</html>
