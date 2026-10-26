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

    // 2. Разбираем параметры ссылки от Advanced URI
    const urlParams = new URLSearchParams(window.location.search);
    
    let file = urlParams.get('filepath') || urlParams.get('file');
    let heading = urlParams.get('heading') || urlParams.get('hash');
    let vault = urlParams.get('vault') || vaultName;

    if (file) {
      // Обязательно убираем расширение .md, если оно прилетело из Advanced URI
      file = file.replace(/\.md$/, '');

      // Собираем прямую ссылку для открытия приложения
      let obsidianUri = "obsidian://open?vault=" + encodeURIComponent(vault) + "&file=" + encodeURIComponent(file);
      
      if (heading) {
        obsidianUri += "%23" + encodeURIComponent(heading);
      }

      // Выводим ссылку на экран на случай блокировки браузером
      const manualLink = document.getElementById('manual-link');
      if (manualLink) {
        manualLink.href = obsidianUri;
        manualLink.style.display = "inline";
      }
      
      document.getElementById('status').innerText = "Открываем файл: " + file;

      // Моментальный вызов приложения
      window.location.href = obsidianUri;
    } else {
      document.getElementById('status').innerText = "Ошибка: В ссылке не передано имя файла (?filepath=...)";
    }
  });
</script>



