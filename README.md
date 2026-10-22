# pavergara.github.io
Portfolio

## Diagramas técnicos (Unreal / U3)

Las fuentes Mermaid viven en `images/diagrams/src/*.mmd` y los SVG publicados en `images/diagrams/`.

Regenerar un diagrama (Node 18+ y Chrome local instalado):

```powershell
$cfg = Join-Path $env:TEMP 'mmdc-puppeteer.json'
$json = @{ executablePath = 'C:\Program Files\Google\Chrome\Application\chrome.exe'; args = @('--no-sandbox','--disable-gpu') } | ConvertTo-Json -Compress
[System.IO.File]::WriteAllText($cfg, $json, (New-Object System.Text.UTF8Encoding($false)))
$env:PUPPETEER_SKIP_DOWNLOAD = '1'
npx --yes @mermaid-js/mermaid-cli@11 -p $cfg -i images/diagrams/src/u3_01_flow.mmd -o images/diagrams/u3_01_flow.svg -t dark -b '#1e1e1e' -w 1600
```

> El archivo de configuración debe guardarse sin BOM; de lo contrario `mermaid-cli` falla al parsear el JSON.

## Previsualización local

```powershell
python -m http.server 8000
```

Abrir `http://localhost:8000/` (el `fetch` de `content/content.json` no funciona desde `file://`).

