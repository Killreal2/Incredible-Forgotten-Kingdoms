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
    // Получаем все параметры, которые пришли из ссылки Roll20
    const currentUrl = window.location.search;

    if (currentUrl && currentUrl.includes('filepath=')) {
      // Собираем ссылку обратно в формат Advanced URI, сохраняя ВСЕ параметры (и блоки, и заголовки)
      let obsidianUri = "obsidian://advanced-uri" + currentUrl;
      
      // Показываем кнопку ручного перехода на случай блокировок браузера
      const manualLink = document.getElementById('manual-link');
      if (manualLink) {
        manualLink.href = obsidianUri;
        manualLink.style.display = "inline";
      }
      
      // Вытягиваем имя файла для красивого отображения на экране
      const urlParams = new URLSearchParams(currentUrl);
      let file = urlParams.get('filepath') || urlParams.get('file');
      if (file) {
        file = decodeURIComponent(file).split('/').pop().replace(/\.md$/, '');
        document.getElementById('status').innerText = "Открываем блок в файле: " + file;
      }

      // Мгновенно запускаем приложение через Advanced URI
      window.location.href = obsidianUri;
    } else {
      document.getElementById('status').innerText = "Ошибка: В ссылке отсутствуют параметры файла.";
    }
  });
</script>
