---
{"dg-publish":true,"title":"Перенаправление в Obsidian...","permalink":"/go/","dgPassFrontmatter":true}
---


<div style="text-align: center; margin-top: 50px; font-family: sans-serif;">
  <h2>Перенаправление в приложение Obsidian...</h2>
  <p id="status">Пожалуйста, подождите, мы ищем вашу заметку.</p>
  <p><a id="manual-link" href="#" style="color: #7743d5; font-weight: bold; display: none;">Нажмите здесь, если приложение не открылось автоматически</a></p>
</div>

<script>
  window.addEventListener('DOMContentLoaded', () => {
    // 1. УКАЖИТЕ ЗДЕСЬ ИМЯ ВАШЕГО ХРАНИЛИЩА (VAULT)
    const vaultName = "Incredible Forgotten Kingdoms";

    const urlParams = new URLSearchParams(window.location.search);
    
    let file = urlParams.get('filepath') || urlParams.get('file');
    let heading = urlParams.get('heading') || urlParams.get('hash');
    let vault = urlParams.get('vault') || vaultName;

    if (file) {
      // 1. Декодируем и очищаем от .md на конце
      let decodedFile = decodeURIComponent(file).replace(/\.md$/, '');
      
      // 2. Склеиваем файл и заголовок через классическую решетку #
      if (heading) {
        let decodedHeading = decodeURIComponent(heading);
        decodedFile += "#" + decodedHeading;
      }

      // 3. Кодируем ВСЮ строку целиком, чтобы слэши внутри папок превратились в %2F, а решетка в %23
      let encodedTarget = encodeURIComponent(decodedFile);

      // Собираем правильный финальный URI
      let obsidianUri = "obsidian://open?vault=" + encodeURIComponent(vault) + "&file=" + encodedTarget;
      
      const manualLink = document.getElementById('manual-link');
      if (manualLink) {
        manualLink.href = obsidianUri;
        manualLink.style.display = "inline";
      }
      
      document.getElementById('status').innerText = "Переходим к: " + decodedFile;

      // Запуск приложения
      window.location.href = obsidianUri;
    } else {
      document.getElementById('status').innerText = "Ошибка: В ссылке не передано имя файла.";
    }
  });
</script>





