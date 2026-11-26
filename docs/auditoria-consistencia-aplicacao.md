# Auditoria de consistência: aplicação, README e documentação

**Data:** 26/11/2026  
**Branch analisada:** `main`  
**Branch desta contribuição:** `docs/auditoria-testes-seguranca`

## Objetivo e limites

Comparar os arquivos versionados da aplicação e sua documentação, executar verificações estáticas possíveis sem alterar o ambiente de produção e registrar o que depende de confirmação no Vercel/n8n.

**Importante:** esta revisão não envia chamados de teste aos webhooks de produção, não altera endpoints, não desativa workflows, não acessa planilhas/caixas de e-mail e não modifica credenciais. Uma leitura de código não comprova a execução real dos serviços externos.

## 1. Divergências confirmadas

| ID | Local | Evidência | Impacto | Correção segura proposta |
|---|---|---|---|---|
| D-01 | `README.md` e árvore da branch `main` | README aponta para `n8n/chatbot-chamados-n8n.json` e manda importá-lo. A árvore consultada não contém a pasta `n8n/` nem o JSON. | A instrução de importação não pode ser seguida a partir do conteúdo atual da branch. | Antes de instruir importação, recuperar o export sanitizado ou deixar explícito que o workflow está apenas na instância n8n e não é reproduzível pelo repositório. |
| D-02 | `README.md` | No início indica `https://sistema-de-triagem-automatica.vercel.app/`; mais adiante indica `https://sistema-de-triagem-eosin.vercel.app/` como demonstração. | Duas URLs são apresentadas como demonstração publicada. | Não escolher uma por suposição. Confirmar com o proprietário da Vercel qual domínio está ligado ao deployment atual; depois padronizar o README. |
| D-03 | `index.html` × `docs/configuracao-n8n.md` | O HTML aponta ambos os webhooks para o host `udf-tendencias-ccp.app.n8n.cloud`. A documentação de configuração cita `testes-udf-vibe-coding.app.n8n.cloud` para o webhook de abertura. | Quem configurar o workflow com base no documento pode usar host diferente do consumido pela página. | Confirmar a Production URL no nó Webhook ativo do n8n. Não substituir a URL do HTML até essa confirmação. |
| D-04 | `README.md` × `docs/casos-de-teste.md` | Ambos descrevem um registro antigo: somente o cenário 1 aprovado com dados simulados e demais pendentes. Existe ao menos um teste posterior relatado em 26/11/2026, descrito neste relatório. | Status da documentação está desatualizado em relação à evidência posterior compartilhada pelo contribuinte. | Consolidar as execuções da equipe em uma matriz única, com resultado observado e evidência. Não marcar todos os testes como aprovados sem seus registros. |
| D-05 | `README.md` × `docs/configuracao-n8n.md` × arquivos versionados | README sugere que o workflow do chatbot está versionado; configuração diz que o JSON do workflow de abertura não foi fornecido. A árvore atual não contém exports de workflow. | Não está claro quais partes da automação podem ser reconstruídas apenas com o Git. | Documentar separadamente workflows exportados/versionados e workflows existentes apenas na conta n8n. |

## 2. Verificações estáticas realizadas no HTML

| ID | Verificação | Resultado da inspeção |
|---|---|---|
| S-01 | URLs configuradas no frontend | Foram localizadas constantes `WEBHOOK_URL` e `CHAT_URL`. Ambas usam o host `udf-tendencias-ccp.app.n8n.cloud`, com caminhos `/webhook/abrir-chamado` e `/webhook/chat-chamado`. |
| S-02 | Validação de campos do formulário | O JavaScript verifica nome com pelo menos 3 caracteres, formato de e-mail, setor selecionado e descrição com pelo menos 20 caracteres. |
| S-03 | Limites de entrada no HTML | Nome: 120; e-mail: 160; descrição: 2.000; mensagem do chat: 1.000 caracteres. |
| S-04 | Resposta de abertura | O frontend só chama a função de exibição de sucesso quando encontra `r.corpo.sucesso === true`; também trata resposta HTTP 422. |
| S-05 | Payload do chatbot | O frontend envia protocolo, e-mail, `sessionId` e mensagem para o webhook de chat. A autorização real precisa ser conferida no workflow n8n. |
| S-06 | Segurança do endpoint | As URLs de webhook estão no JavaScript do navegador e, portanto, são visíveis ao público. URL não deve ser considerada segredo ou autenticação. |

Essas verificações são estáticas: confirmam o que está escrito no HTML, não a execução do código nem a configuração do servidor.

## 3. Testes de execução possíveis e não possíveis nesta revisão

### Resultado observado compartilhado pelo contribuinte

Em 26/11/2026, o contribuinte compartilhou uma execução na aplicação publicada: a abertura retornou sucesso, gerou protocolo, classificou o problema como Software/Média e exibiu resumo e sugestão inicial coerentes. O conteúdo da confirmação por e-mail foi compartilhado, mas a entrega na caixa de entrada não foi verificada independentemente. Nome, endereço de e-mail e protocolo completo foram omitidos por privacidade.

### Não verificados nesta revisão

- Acesso independente aos dois domínios Vercel e identificação do deployment atualmente ativo.
- POST de teste aos webhooks de produção.
- Production URLs efetivas e estado Published/Active dos workflows no n8n.
- Persistência do chamado na planilha Google Sheets.
- Entrega efetiva de e-mail e alerta de prioridade alta.
- Fallback com modelo indisponível.
- Autorização do chatbot com protocolo válido e e-mail incorreto.
- Proteção contra consulta de chamados de terceiros.
- Tratamento de falha de Sheets/Gmail.

Não foram executados testes destrutivos nem tentativas de derrubar integrações de produção.

## 4. Ações pendentes antes de alterar endereços

1. O responsável pela Vercel deve confirmar qual URL é o deployment oficial e se ambos os domínios ainda apontam para a aplicação.
2. O responsável pelo n8n deve copiar as Production URLs diretamente dos nós Webhook ativos de abertura e chat.
3. Comparar os endereços confirmados com as constantes do HTML.
4. Só então alterar a documentação e, se necessário, o HTML, em commit separado.
5. Fazer novo teste de abertura e chat depois de qualquer alteração de endpoint.

## 5. Recomendação para a documentação

Manter este relatório como histórico da auditoria e atualizar `docs/casos-de-teste.md` somente com execuções que tenham resultado observado e evidência suficiente. O status geral não deve ser declarado como “todos os testes aprovados” enquanto houver cenários sem registro verificável.

## 6. Segurança e preservação da aplicação

- Não alterar endpoints de produção por inferência.
- Não publicar credenciais, tokens, dados pessoais ou planilhas com chamados reais.
- Não remover nem desativar nós do n8n para testar falhas em produção.
- Fazer mudanças primeiro em branch e submeter por Pull Request.
- Após confirmar URLs, alterar somente os endereços divergentes, sem refatorar o formulário ou os workflows.
