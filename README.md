# Blackline-Scan-browser
Web Scanner perfeito para navegadores! 🚀  

# 🕵️ BlackLine Scanner

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

## 📢 Apresentação  
Venho apresentar um **Web Scanner perfeito para navegadores!** 🚀  

O scanner faz uma busca completa na aplicação web e traz os resultados **instantaneamente**, facilitando sua vida de **bug hunter** e **pentester**, ajudando a encontrar **URLs, diretórios e arquivos ocultos**.  

> ⚠️ **Nota:** Este script **não** faz uma busca super profunda, mas é um ótimo complemento para outras ferramentas como **Waybackurls, GAU, GAUplus**.


## 🔍 **Código do Scanner**
## Copie:  

```javascript
javascript:void(function(){
    let e = document.createElement('div');
    e.style.cssText = 'position:fixed;bottom:0;left:0;width:100%;height:300px;background:#1a1a1a;color:#00ff00;z-index:999999;padding:20px;overflow:auto;font-family:monospace;';
    e.innerHTML = '<h3 style="color:#00ff00">🔍 BlackLine Scanner</h3><div id="results">Scanning...</div>';
    document.body.appendChild(e);
    
    let currentDomain = window.location.hostname;
    let foundUrls = new Set();
    
    function findUrls() {
        let urls = [];
        let sources = [...document.getElementsByTagName('a'), ...document.getElementsByTagName('script'),
                       ...document.getElementsByTagName('img'), ...document.getElementsByTagName('link'), 
                       ...document.getElementsByTagName('form')];
        
        sources.forEach(element => {
            if (element.href) urls.push(element.href);
            if (element.src) urls.push(element.src);
            if (element.action) urls.push(element.action);
        });

        let content = document.documentElement.innerHTML;
        let urlPattern = /(?:url\(|href="|src="|action="|url:|endpoint:|path:|route:)\s*['"]?([^'"\)\s>]+)/gi;
        let match;
        
        while ((match = urlPattern.exec(content)) !== null) {
            if (match[1] && !match[1].startsWith('data:')) urls.push(match[1]);
        }

        let scriptPattern = /"[^"]*"|'[^']*'/g;
        let scripts = document.documentElement.innerHTML.match(scriptPattern) || [];
        
        scripts.forEach(script => {
            let urlMatches = script.match(/(?:\/[a-zA-Z0-9_-]+)+(?:\.[a-zA-Z0-9]+)?/g) || [];
            urlMatches.forEach(url => urls.push(url));
        });

        performance.getEntriesByType('resource').forEach(entry => urls.push(entry.name));
        
        return [...new Set(urls)];
    }
    
    let allUrls = findUrls();
    allUrls.sort();
    
    document.getElementById('results').innerHTML = 
        `<div style="margin:10px 0;color:#00ff00">✅ Found ${allUrls.length} URLs & Endpoints on ${currentDomain}</div>
        <div style="background:#2a2a2a;padding:10px;border-radius:5px">
        ${allUrls.map(url => `<div style="color:white;margin:5px 0;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}
        </div>`;
})();

```

## Script Interface:


![image](https://i.postimg.cc/pdB4p3Fc/Captura-de-tela-2025-01-31-124535.png)


## Etapas Para a Instalação

### 1 - Com o Script em mãos, clique com o botão direito na barra do navegador e adicione aos favoritos.
### 2 - Cole o Script na área de URL do favorito e salve.
### 3 - O favorito aparecerá na barra de Favoritos. Basta clicar nele e usar o script.




**Créditos**: Desconhecido  
# **By**: Ivarsatierf

 Aproveitem o scan!
