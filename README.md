# TudoPronto PDF

Website estático bilingue (PT/EN) com nove ferramentas PDF executadas no navegador.

## Funcionalidades

- Juntar PDF: combina dois ou mais PDFs.
- Dividir PDF: extrai páginas indicadas (ex.: `1-3,5`).
- Comprimir PDF: regrava/otimiza a estrutura e compara o tamanho. **pdf-lib não recomprime necessariamente imagens já embutidas**; se o resultado não for menor, o site informa e não apresenta uma falsa redução.
- Rodar PDF: roda todas as páginas em incrementos de 90°.
- PDF para imagens: renderiza páginas em PNG/JPG e descarrega um ZIP.
- Imagens para PDF: cria um PDF a partir de imagens PNG/JPG/WEBP.
- Organizar páginas: recebe a ordem completa (ex.: `3,1,2`).
- Eliminar páginas: remove as páginas indicadas.\n- Texto para PDF: transforma texto escrito ou colado no navegador num PDF A4, com título opcional e quebra automática de linhas e páginas.

## Bibliotecas

As bibliotecas PDF-Lib, PDF.js e JSZip são carregadas de CDNs públicos (jsDelivr e cdnjs). Isso requer ligação à Internet na primeira utilização e significa que o código dessas bibliotecas é obtido de terceiros. Os documentos selecionados não são enviados para esses CDNs: o processamento é local no navegador.

## Executar localmente

Abra `index.html` num navegador moderno. Para melhor compatibilidade com módulos/ficheiros e para testar como num alojamento real, pode iniciar um servidor estático local:

```bash
python -m http.server 8000
```

Depois visite `http://localhost:8000`.

## Publicar no GitHub Pages

1. Crie um repositório GitHub e carregue o conteúdo desta pasta para a raiz do repositório.
2. Abra **Settings → Pages**.
3. Em **Build and deployment**, escolha **Deploy from a branch**, selecione `main` e `/ (root)`.
4. Guarde e aguarde o URL publicado.

## Publicar no Cloudflare Pages

1. Crie um projeto Pages e ligue o repositório GitHub, ou carregue diretamente os ficheiros.
2. Framework preset: **None**.
3. Build command: vazio (ou sem comando).
4. Build output directory: `/` ou a pasta raiz do projeto, conforme o método de publicação.

## Antes de publicar

- Substitua `YOUR-DOMAIN.example` em `sitemap.xml` e `robots.txt` pelo domínio final (com HTTPS).
- Configure um endereço de contacto real em `contact.html` e o link `mailto:` em `index.html`.
- Atualize as políticas legais com os dados do operador e as regras aplicáveis ao país/mercado onde o site será disponibilizado.
- Verifique a política de privacidade e consentimento antes de instalar qualquer rede de anúncios ou analytics. O espaço publicitário da página inicial é apenas um marcador visual; não contém anúncios.
- Defina um domínio canónico e acrescente metadados específicos se usar domínio próprio.

## Limitações conhecidas

- PDFs protegidos por palavra-passe, danificados ou com estruturas incomuns podem não abrir.\n- Texto para PDF utiliza as fontes padrão Helvetica do PDF; caracteres fora do conjunto suportado por essas fontes podem não ser convertidos corretamente.
- A compressão por regravação não garante redução. Para uma compressão real de imagens seria necessária uma rotina adicional de rasterização/recompressão, com possível perda de qualidade.
- A conversão PDF → imagem usa memória proporcional ao número e à resolução das páginas; ficheiros grandes podem exceder os limites do dispositivo. Use escala 1× para documentos longos.
- As bibliotecas são carregadas de CDN; esta versão não inclui cópias locais/offline dessas dependências.
- A tradução PT/EN está aplicada à interface principal e às ferramentas. As páginas legais adicionais estão em português nesta versão inicial.

## Segurança e privacidade

O código não implementa upload de documentos. A operação é executada com File API, PDF-Lib, PDF.js, Canvas e JSZip no cliente. A entrega de resultados usa URLs Blob locais revogadas após o download.

## Verificação realizada nesta entrega

- `app.js` passou a verificação de sintaxe JavaScript (`node --check`).
- A tentativa de teste automatizado em Chromium não pôde navegar para o servidor local neste ambiente de execução (bloqueio de navegação `ERR_BLOCKED_BY_ADMINISTRATOR`). Por isso, não afirmo que foi concluído um teste funcional real de ponta a ponta das oito operações. Recomenda-se testar cada ferramenta no navegador após publicar ou executar localmente, usando PDFs de teste próprios.
