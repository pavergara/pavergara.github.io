# pavergara.github.io
Portfolio

## Diagramas técnicos (Unreal / U3)

Las fuentes Mermaid viven en `images/diagrams/src/` (`u3_01_flow.en.mmd`, `u3_01_flow.es.mmd`, `u3_01_sequence.en.mmd`, `u3_01_sequence.es.mmd`) y los SVG publicados en `images/diagrams/` (`u3_01_flow_en.svg`, `u3_01_flow_es.svg`, etc.).

Los nombres de clases, nodos y dispatchers se mantienen sin traducir; solo cambian los textos descriptivos. El sitio intercambia el `src` de cada diagrama mediante `data-i18n-src` y las claves `u3_img_flow` / `u3_img_seq` de `content.json`.

Regenerar un diagrama (Node 18+ y Chrome local instalado):

```powershell
$cfg = Join-Path $env:TEMP 'mmdc-puppeteer.json'
$json = @{ executablePath = 'C:\Program Files\Google\Chrome\Application\chrome.exe'; args = @('--no-sandbox','--disable-gpu') } | ConvertTo-Json -Compress
[System.IO.File]::WriteAllText($cfg, $json, (New-Object System.Text.UTF8Encoding($false)))
$env:PUPPETEER_SKIP_DOWNLOAD = '1'
npx --yes @mermaid-js/mermaid-cli@11 -p $cfg -i images/diagrams/src/u3_01_flow.en.mmd -o images/diagrams/u3_01_flow_en.svg -t dark -b '#1e1e1e' -w 1600
```

> El archivo de configuración debe guardarse sin BOM; de lo contrario `mermaid-cli` falla al parsear el JSON.

## Previsualización local

```powershell
python -m http.server 8000
```

Abrir `http://localhost:8000/` (el `fetch` de `content/content.json` no funciona desde `file://`).

