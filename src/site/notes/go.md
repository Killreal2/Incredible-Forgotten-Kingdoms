---
{"dg-publish":true,"title":"Перенаправление в Obsidian...","dg-show-sidebar":false,"permalink":"/go/","dgPassFrontmatter":true}
---


<div style="text-align: center; margin-top: 50px; font-family: sans-serif;">
  <h2>Перенаправление в приложение Obsidian...</h2>
  <p id="status">Пожалуйста, подождите, мы ищем вашу заметку.</p>
  <p><a id="manual-link" href="#" style="color: #7743d5; font-weight: bold; display: none;">Нажмите здесь, если приложение не открылось автоматически</a></p>
</div>

<script>
  window.addEventListener('DOMContentLoaded', () => {
    const currentUrl = window.location.search;

    if (currentUrl && currentUrl.includes('filepath=')) {
      let obsidianUri = "obsidian://advanced-uri" + currentUrl;
      
      const manualLink = document.getElementById('manual-link');
      if (manualLink) {
        manualLink.href = obsidianUri;
        manualLink.style.display = "inline";
      }
      
      const urlParams = new URLSearchParams(currentUrl);
      let file = urlParams.get('filepath') || urlParams.get('file');
      if (file) {
        file = decodeURIComponent(file).split('/').pop().replace(/\.md$/, '');
        document.getElementById('status').innerText = "Открываем блок в файле: " + file;
      }

      // 1. Запускаем Obsidian
      window.location.href = obsidianUri;

      // 2. Ускоренный таймер автозакрытия вкладки на 1800 мс (1,8 секунды)
      setTimeout(() => {
        document.getElementById('status').innerText = "Готово! Возвращайтесь к игре в Roll20.";
        
        // Пытаемся закрыть вкладку
        window.close();
        
        // Резервный вариант закрытия
        window.open('', '_self', '').close();
      }, 1800);

    } else {
      document.getElementById('status').innerText = "Ошибка: В ссылке отсутствуют параметры файла.";
    }
  });
</script>
