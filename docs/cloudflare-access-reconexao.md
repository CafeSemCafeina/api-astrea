# Guia de aparência e reconexão do Cloudflare Access para Astrea

Status: guia versionado para revisão. A aplicação manual no Cloudflare Access não foi feita.

Este guia registra uma apresentação Syntelix para o login do Access e um roteiro de reconexão da integração Astrea. O pacote contém somente este documento e o logo copiado para a documentação. Ele não altera políticas, provedores de identidade, credenciais, duração de sessão, transporte API, código ou deploy.

Os campos de organização são globais. Uma alteração de nome, logo, cabeçalho, rodapé ou fundo pode aparecer em todas as aplicações da organização. O nome exibido da aplicação e a mensagem de bloqueio padrão são campos separados e devem ser revisados por aplicação.

## Use a fonte visual canônica

O fundo oficial para este guia é `paper`, `#f4f0ea`. Ele substitui o fundo provisório `#F5F7FA` usado no plano anterior. Os papéis de apoio são `paper-light` (`#faf8f4`), `ink` (`#211b25`), `purple-600` (`#673981`) e `purple-700` (`#4b295e`). A tipografia de referência é Source Serif 4 para tese e destaque, Inter para corpo e controles, e JetBrains Mono para metadados.

As referências abaixo estão fixadas no commit publicado `b09c58894a21996927aaa1f6bc0911ff0f459db7` do repositório canônico e foram verificadas pela API GitHub autenticada em 06/10/2026. O repositório é privado e requer acesso autorizado.

- [Resumo de identidade](https://github.com/Syntelix-AI/syntelix-web/blob/b09c58894a21996927aaa1f6bc0911ff0f459db7/docs/DESIGN.md)
- [Sistema de design](https://github.com/Syntelix-AI/syntelix-web/blob/b09c58894a21996927aaa1f6bc0911ff0f459db7/DESIGN.md)
- [Tokens implementados](https://github.com/Syntelix-AI/syntelix-web/blob/b09c58894a21996927aaa1f6bc0911ff0f459db7/app/app.css)
- [Logo oficial na referência publicada](https://github.com/Syntelix-AI/syntelix-web/blob/b09c58894a21996927aaa1f6bc0911ff0f459db7/public/brand/syntelix-logo.png)

A consulta original usou o commit local `9381d1b4f81c62ab7d45fcec533516cf80547cb3`, indisponível no GitHub. Os quatro arquivos acima têm os mesmos blobs Git nos dois commits; a referência publicada preserva integralmente os documentos, tokens e logo consultados. Nenhum commit do projeto de origem foi publicado por este pacote.

Use o [logo local da documentação](assets/brand/syntelix-logo.png) como o ativo aprovado para revisão. O arquivo deve manter o SHA-256 `9d4d7757529237e971e84c2f12182a8a9ad48d40f5eb10c0bf1b222515992b15`. Copiar o arquivo para este repositório não publica uma URL de logo. O painel precisa confirmar a URL de ativo aprovada, o tamanho, o formato e os limites de texto aceitos pelo campo nativo.

## Preencha somente os campos nativos documentados

Use os campos globais de nome da organização, logo, cabeçalho, rodapé e cor de fundo. Use o nome exibido e a mensagem de bloqueio na aplicação correspondente. O Cloudflare documenta esses campos e o alcance global na [página de login personalizada](https://developers.cloudflare.com/cloudflare-one/reusable-components/custom-pages/access-login-page/).

No painel, abra `Zero Trust > Reusable components > Custom pages > Access login page > Manage` para revisar os campos globais. Na aplicação existente, abra `Additional settings > Custom block pages > Cloudflare default` para revisar a mensagem por aplicação e confira o tipo antes de editar.

O Access não documenta controles para escolher a fonte, mudar o layout inteiro, controlar a cor dos botões, traduzir todos os erros nativos ou aplicar CSS arbitrário à página de login. Este pacote não injeta CSS e não cria uma tela de login paralela.

A mensagem de bloqueio usa a opção de mensagem personalizada da página padrão. O template HTML de bloqueio hospedado é uma opção diferente, disponível somente nos planos Pay-as-you-go e Enterprise conforme a [documentação da página de bloqueio](https://developers.cloudflare.com/cloudflare-one/reusable-components/custom-pages/access-block-page/). O plano atual e os limites do campo precisam ser conferidos no painel.

## Configure a cópia compartilhada

Use estes valores nos campos globais, depois de revisar o preview de todas as aplicações afetadas:

| Campo | Valor |
| --- | --- |
| Nome da organização | `Syntelix` |
| Cabeçalho | `Conecte sua integração Syntelix` |
| Rodapé | `Use o e-mail combinado com a equipe. Confira sua caixa de entrada e o spam. Ao concluir, volte ao aplicativo. Nunca compartilhe o código.` |
| Rodapé curto, se o campo exigir menos texto | `Use o e-mail combinado com a equipe. Ao concluir, volte ao aplicativo. Nunca compartilhe o código.` |
| Fundo | `#f4f0ea` |

Não coloque `Kommo`, `Astrea`, nome de pessoa, e-mail ou regra de autorização no cabeçalho global. Os campos globais precisam continuar adequados para todas as aplicações da organização.

## Configure o nome e a mensagem do Astrea

Proponha o nome exibido `Syntelix · Astrea`. Confirme no painel que o nome distingue o tenant correto e não conflita com outra aplicação. Use um identificador de serviço, sem dados pessoais.

Na opção de mensagem personalizada da página de bloqueio padrão, proponha exatamente:

`Não foi possível concluir o acesso ao Astrea. Confira o e-mail usado ou peça ajuda à equipe Syntelix. Não envie seu código.`

Essa mensagem é específica da aplicação. Ela não altera a regra de acesso e não é um template HTML premium. Um endereço não autorizado pode continuar vendo a tela genérica de envio do OTP, e essa tela não garante que a página de bloqueio será exibida.

Este roteiro só se aplica quando uma implantação externa do Access e o cliente usado oferecerem esse fluxo. O `main` deste worktree não implementa essa passagem. Trate qualquer handoff como uma dependência a verificar.

## Oriente a reconexão pelo cliente real

Entregue estas instruções no cliente que inicia a autorização:

1. Inicie a reconexão no cliente real da integração Astrea.
2. Conclua o fluxo na mesma instância do navegador que o cliente abriu.
3. Use o e-mail combinado com a equipe Syntelix.
4. Se o código não chegar, confira o endereço, a caixa de entrada, o spam e a quarentena.
5. Se você pedir outro código, use o código mais recente.
6. Ao concluir o acesso, volte ao cliente e confirme que a integração aparece como conectada.
7. Se o estado continuar pendente, informe o serviço, o horário com fuso e a mensagem de erro à equipe Syntelix.

Não envie o código, o token, cookies ou a URL completa de autenticação. Não reinicie o fluxo em outra janela para contornar um estado pendente.

## Registre os limites do OTP

O OTP expira dez minutos depois da solicitação inicial e pode ser usado uma vez. Pedir outro código invalida o código anterior. Esses comportamentos estão descritos na [documentação oficial do One-time PIN](https://developers.cloudflare.com/cloudflare-one/integrations/identity-providers/one-time-pin/).

A tela genérica que diz que o código foi enviado não prova o envio, a entrega ou o destinatário. O log de autenticação só aparece depois que o usuário envia o código. Nenhuma causa da ausência histórica de código foi confirmada por este pacote. Filtragem, quarentena, supressão ou consumo antecipado continuam hipóteses que exigem evidência.

Não amplie allowlists e não teste como uma cliente. Qualquer solicitação futura de OTP precisa de uma conta de teste e de autorização explícita do responsável por essa conta.

## Preserve os limites da base Astrea

O `main` documentado neste worktree oferece o transporte MCP remoto em `/mcp`, protegido pelo header `x-api-key`, conforme a seção [MCP remoto do README](../README.md#mcp-remoto). Esta base não contém um proxy Access nem um callback OAuth. Não há `cf-worker/` ou `wrangler.jsonc` neste `main`, portanto este guia não cria links para esses caminhos.

Quando existir uma implantação externa do Access, verifique separadamente a passagem do cliente para essa implantação, o retorno ao cliente Astrea e a persistência da conexão. O login no navegador não prova que o cliente consegue usar a sessão. A identidade do Access, a conta do sistema Astrea que fornece os dados, a identidade ou conta do provedor de login, a chave API e uma eventual sessão MCP ou OAuth são camadas diferentes.

## Aplique a apresentação somente após revisão

Quando houver acesso administrativo aprovado, siga esta sequência manual:

1. Faça um inventário somente de leitura das aplicações afetadas, da configuração atual, do plano e dos campos disponíveis. Registre o impacto global.
2. Confira o preview nativo com o fundo `#f4f0ea`, o logo, a cópia compartilhada, o nome `Syntelix · Astrea` e a mensagem de bloqueio.
3. Aprove a apresentação e confirme que o nome não conflita com outro tenant. Defina também um canal de ajuda sem incluir dados pessoais.
4. Aplique somente os campos visuais aprovados. Guarde os valores anteriores para reversão.
5. Execute a matriz de aceitação abaixo com o cliente real e uma conta de teste autorizada.
6. Registre evidência sanitizada com data, fuso, serviço, versão do cliente, estado esperado, estado observado e erro. Remova códigos, tokens, cookies, e-mails completos e parâmetros da URL.

Não execute scripts de provisionamento ou deploy para alterar a aparência. Não crie payload de escrita para uma API que não esteja documentada. Não altere políticas, IdPs, callbacks ou duração de sessão neste passo.

Se uma ajuda externa ou um redirecionamento for escolhido no futuro, use uma URL genérica aprovada e confira os parâmetros realmente transmitidos. Não presuma uma garantia geral da plataforma.

## Aceitação futura, ainda não executada

Todos os casos abaixo estão planejados. Nenhum caso foi executado por este pacote. O cliente real precisa iniciar e concluir cada fluxo. Um login bem-sucedido somente no navegador do Access não conta como reconexão.

| Caso | Critério |
| --- | --- |
| Reconexão Astrea | Iniciar no cliente, completar o mecanismo Access externo quando existir, retornar ao cliente e comprovar uma consulta MCP de leitura. Registrar como bloqueado se o cliente não suportar o handoff. |
| Endereço não autorizado | Continuar negado. A tela genérica de envio pode aparecer, mas não prova entrega e não exige bloqueio imediato. |
| Código expirado | Rejeitar o código após dez minutos e permitir uma nova tentativa controlada. |
| Código reenviado | Rejeitar o código anterior e aceitar somente o código novo válido. Não registrar os valores. |
| PIN já consumido | Se a implantação externa efetiva usar OTP, rejeitar a reutilização de um PIN já consumido. Registrar como inaplicável se o mecanismo implantado não usar OTP. Não registrar o valor. |
| Expiração independente | O `main` deste worktree oferece API-key em `/mcp` e não implementa Access ou OAuth. Se uma implantação externa efetiva adicionar camadas Access e OAuth/MCP independentes, testar Access expirado com OAuth/MCP válido e o inverso. Registrar como inaplicável enquanto essas camadas não existirem ou não forem independentes. |
| Login completo | Retornar ao cliente correto, mostrar estado conectado e executar uma consulta de leitura sem alterar dados. |
| Fluxo interrompido | Cancelar ou fechar o fluxo, reiniciar pelo cliente e confirmar que nenhum acesso foi concedido por engano. |
| Apresentação | Conferir logo, contraste, teclado e viewport estreito no preview nativo. |
| Privacidade | Não mostrar dados pessoais, lista de usuários, códigos, tokens ou URLs completas na evidência. |

O responsável pela conta de teste autoriza cada solicitação de OTP. Alterações de código e extensões de sessão ficam fora desta aceitação.

## Feche as decisões pendentes antes de aplicar

- Acesso ao painel e configuração atualmente implantada.
- Hospedagem do ativo, URL aprovada, tamanho, formato e limites dos campos nativos.
- Unicidade de `Syntelix · Astrea` e canal de ajuda.
- Suporte do cliente Astrea ao handoff externo e confirmação de que a base implantada corresponde ao `main` documentado.
- Inclusão de e-mail em políticas, que permanece em uma tarefa separada.
- Google, autenticação instantânea e duração de sessão. Cada opção exige aprovação separada.

Este documento descreve o que revisar e testar. Ele não afirma que uma aplicação Access foi criada, que a marca foi publicada, que um proxy foi implantado ou que o fluxo Astrea está integrado ao Access.

## Fontes oficiais usadas

- [Página de login personalizada](https://developers.cloudflare.com/cloudflare-one/reusable-components/custom-pages/access-login-page/)
- [Página de bloqueio personalizada](https://developers.cloudflare.com/cloudflare-one/reusable-components/custom-pages/access-block-page/)
- [Aplicação SaaS com OIDC genérico](https://developers.cloudflare.com/cloudflare-one/access-controls/applications/http-apps/saas-apps/generic-oidc-saas/)
- [Aplicação pública self-hosted](https://developers.cloudflare.com/cloudflare-one/access-controls/applications/http-apps/self-hosted-public-app/)
- [One-time PIN](https://developers.cloudflare.com/cloudflare-one/integrations/identity-providers/one-time-pin/)
- [Diagnóstico do Access](https://developers.cloudflare.com/cloudflare-one/troubleshooting/access/)
