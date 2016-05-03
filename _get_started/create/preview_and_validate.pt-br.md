---
layout: page
title: Visualizar e validar
order: 3
locale: pt-br
---

Visualize a página AMP exatamente como visualizaria qualquer outro site HTML estático. Não é necessário uma etapa de compilação ou de pré-processamento. Uma das possibilidades:

  - **Abra a página diretamente no navegador a partir do sistema de arquivos** (certos elementos podem não funcionar devido a uma falha de XMLHttpRequests)
  - **Use um servidor da Web local, como o Apache 2 ou Nginx**.
    *(Tip: Para um servidor da Web rápido, execute `python -m SimpleHTTPServer`.)*

Depois, certifique-se de que sua página AMP** seja realmente válida para AMP**, caso contrário, ela não será descoberta e distribuída por plataformas de terceiros como a Pesquisa do Google. Para validar:

  1. Abra sua página no navegador.
  1. Adicione "`#development=1`“ ao URL, por exemplo,`http://localhost:8000/released.amp.html#development=1`.
  1. Abra o [console Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/debug/console/) e verifique se há erros de validação.

[Saiba mais sobre validação](/docs/guides/validate.html) e o que fazer quando ocorrerem erros.

{% include button.html title="Continuar para a etapa 5" link="/docs/get_started/create/prepare_for_discovery.pt-br.html" %}
