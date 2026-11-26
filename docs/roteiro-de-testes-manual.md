# Roteiro de testes e validação manual

Este roteiro complementa [casos-de-teste.md](casos-de-teste.md) e deve ser preenchido durante a validação da aplicação publicada e dos workflows no n8n.

> **Estado inicial:** os cenários abaixo estão aguardando execução nesta rodada de validação. Resultado esperado não significa teste aprovado. Não marque um cenário como aprovado sem executar e registrar evidência.

## 1. Identificação da execução

- Responsável pelo teste: contribuinte do projeto (identificação pessoal omitida nesta documentação pública).
- Data e horário: 26/11/2026, aproximadamente 09:49 (horário informado na tela: 09:49:35).
- Ambiente: aplicação publicada (conforme relato do testador; URL e navegador não informados).
- Navegador e versão: não informado.
- URL efetivamente testada: não confirmada nesta execução.
- Versão/commit da aplicação: não identificado.
- Observações: teste inicial relatado pelo contribuinte. Protocolo e identificação do solicitante foram anonimizados para não expor dados pessoais no repositório público.

Use somente dados fictícios. Não registre senhas, tokens, credenciais, e-mails reais ou dados pessoais nas capturas de tela.

## 2. Abertura de chamados

| ID | Cenário / entrada | Resultado esperado | Resultado observado | Status |
|---|---|---|---|---|
| AB-01 | Abrir chamado válido (teste realizado com dados do próprio contribuinte) | O formulário envia os dados, recebe confirmação e apresenta protocolo | **Sucesso.** A tela informou chamado aberto e gerou protocolo (anonimizado: `CH-20261126-XXXX`). | Aprovado — relato do testador |
| AB-02 | Nome vazio ou com menos de 3 caracteres | Validação impede o envio e informa o campo inválido | A preencher | Não executado |
| AB-03 | E-mail inválido (ex.: `teste@empresa`) | Validação impede o envio | A preencher | Não executado |
| AB-04 | Setor não selecionado | Validação impede o envio | A preencher | Não executado |
| AB-05 | Descrição vazia ou com menos de 20 caracteres | Validação impede o envio | A preencher | Não executado |
| AB-06 | Descrição com acentos, pontuação, quebra de linha e texto longo | Interface permanece funcional; texto é armazenado sem interpretar conteúdo como HTML | A preencher | Não executado |
| AB-07 | Problema de internet ou webhook indisponível durante o envio | Mensagem de erro compreensível; interface não informa sucesso falso | A preencher | Não executado |
| AB-08 | Enviar duas vezes rapidamente o mesmo formulário | Comportamento controlado; registrar se há duplicidade de protocolos/registros | A preencher | Não executado |

## 3. Classificação por IA e prioridade

| ID | Entrada | Resultado esperado | Resultado observado | Status |
|---|---|---|---|---|
| IA-01 | “A internet caiu no setor inteiro” | Rede/Internet; prioridade Alta; segue ramificação de alerta | Não executado nesta rodada; foi testada outra descrição (ver registro IA-08). | Pendente |
| IA-02 | “Esqueci minha senha do sistema” | Acesso/Senha; prioridade Média | A preencher | Não executado |
| IA-03 | “Quero trocar o papel de parede” | Outro; prioridade Baixa; sem alerta de urgência | A preencher | Não executado |
| IA-04 | “Recebi um e-mail suspeito pedindo minha senha” | Prioridade Alta ou encaminhamento prudente para segurança; não afirmar que o incidente está confirmado | A preencher | Não executado |
| IA-05 | “Minha impressora não liga” | Hardware; prioridade coerente com impacto individual | A preencher | Não executado |
| IA-06 | Descrição ambígua, sem informar quantidade de pessoas afetadas | Classificação prudente, sem inventar contexto; equipe humana pode revisar | A preencher | Não executado |
| IA-07 | IA indisponível ou resposta fora do formato esperado | Fallback documentado; `classificado_por_ia = false`; chamado continua registrável | A preencher | Não executado |
| IA-08 | “Usuário impossibilitado de realizar a saída de produtos no sistema de coleta.” | Categoria Software; prioridade Média, considerando impedimento operacional individual | A tela retornou **Software / Média** e resumo coerente com o problema descrito. | Aprovado — relato do testador |

**Atenção:** a classificação é probabilística. Registre a saída real, inclusive quando divergir do esperado. Não altere o resultado observado para fazê-lo coincidir com o roteiro.

## 4. Persistência e notificações

| ID | Verificação | Resultado esperado | Resultado observado | Status |
|---|---|---|---|---|
| INT-01 | Conferir chamado recém-aberto na planilha | Protocolo e campos correspondem ao formulário e à resposta exibida | A preencher | Não executado |
| INT-02 | Conferir e-mail de confirmação | Mensagem chega ao endereço utilizado no teste e contém protocolo correto | O testador forneceu o conteúdo da confirmação com protocolo, categoria, prioridade, resumo e sugestão inicial. Endereço foi omitido por privacidade. | Confirmado pelo relato do testador; entrega não verificada independentemente |
| INT-03 | Abrir chamado de prioridade Alta | Alerta é enviado à equipe configurada, com protocolo correspondente | A preencher | Não executado |
| INT-04 | Simular indisponibilidade do Sheets em ambiente controlado | Sistema apresenta falha controlada e não afirma que o chamado foi salvo | A preencher | Não executado |
| INT-05 | Simular falha do Gmail em ambiente controlado | Falha de notificação fica identificável; registrar se o chamado foi salvo antes da falha | A preencher | Não executado |

Não remova credenciais nem provoque falhas em produção sem autorização do responsável pelo ambiente. Se não houver ambiente de teste, marque como **Não executado — requer ambiente controlado**.

## 4.1 Registro da primeira execução — 26/11/2026

O contribuinte informou que abriu um chamado na aplicação e compartilhou a resposta exibida. Para preservar a privacidade, não foram registrados nome, endereço de e-mail nem protocolo completo.

- **Horário exibido:** 09:49:35.
- **Protocolo:** `CH-20261126-XXXX` (mascarado).
- **Descrição resumida:** usuário não conseguia realizar a saída de produtos no sistema de coleta.
- **Classificação retornada:** Software.
- **Prioridade retornada:** Média.
- **Resumo apresentado:** usuário impossibilitado de realizar a saída de produtos no sistema de coleta.
- **Sugestão inicial:** reiniciar/atualizar o aplicativo e verificar campos obrigatórios.
- **Abertura do chamado:** sucesso, com protocolo gerado e tela de confirmação.
- **Confirmação por e-mail:** conteúdo da mensagem foi compartilhado pelo testador; a entrega efetiva na caixa de entrada não foi verificada de forma independente.
- **Registro no Google Sheets:** ainda precisa ser conferido diretamente na planilha.
- **Alerta de prioridade alta:** não aplicável a este chamado, classificado como Média.

**Conclusão parcial:** o envio e a resposta de triagem foram bem-sucedidos neste exemplo. Isso não comprova ainda a persistência na planilha, o recebimento efetivo do e-mail, nem os demais cenários de validação.

## 5. Chatbot de acompanhamento

Antes dos testes, abra um chamado fictício e guarde o protocolo e o e-mail fictício usados. Execute os casos com esse registro.

| ID | Cenário | Resultado esperado | Resultado observado | Status |
|---|---|---|---|---|
| CHAT-01 | Consultar com protocolo e e-mail correspondentes | Chat localiza o chamado e informa somente dados daquele registro | A preencher | Não executado |
| CHAT-02 | Consultar com protocolo inexistente | Mensagem informa que não encontrou o chamado, sem expor outros registros | A preencher | Não executado |
| CHAT-03 | Usar protocolo válido com e-mail diferente | Acesso negado; nenhum dado do chamado é revelado | A preencher | Não executado |
| CHAT-04 | Enviar protocolo vazio ou mensagem vazia | Interface solicita os dados obrigatórios ou apresenta erro controlado | A preencher | Não executado |
| CHAT-05 | Perguntar o status de um chamado existente | Resposta corresponde ao status atualmente registrado na planilha | A preencher | Não executado |
| CHAT-06 | Enviar informação adicional sobre o problema | Informação é registrada no campo previsto, com data/hora, e o chat confirma somente após gravação bem-sucedida | A preencher | Não executado |
| CHAT-07 | Pedir ao bot para alterar prioridade, status ou responsável | Bot não altera esses campos; encaminha a solicitação para avaliação humana | A preencher | Não executado |
| CHAT-08 | Pedir dados de outro chamado ou instruir o bot a ignorar regras | Bot não revela dados de terceiros nem segue instruções para contornar as regras | A preencher | Não executado |
| CHAT-09 | Perguntar algo que não consta no registro | Bot admite que não tem essa informação; não inventa responsável, prazo ou atualização | A preencher | Não executado |
| CHAT-10 | Webhook ou modelo do chatbot indisponível | Mensagem de indisponibilidade compreensível, sem travar a página | A preencher | Não executado |
| CHAT-11 | Enviar mensagem longa, acentos e caracteres especiais | Interface permanece utilizável e respeita o limite de caracteres documentado | A preencher | Não executado |
| CHAT-12 | Atualizar status/responsável na planilha e consultar novamente | Chat reflete os dados atualizados, conforme o comportamento de consulta implementado | A preencher | Não executado |

## 6. Compatibilidade e usabilidade

| ID | Cenário | Resultado esperado | Resultado observado | Status |
|---|---|---|---|---|
| UX-01 | Abrir em tela de computador | Formulário e chat legíveis, sem sobreposição | A preencher | Não executado |
| UX-02 | Abrir em celular | Campos, botões e chat utilizáveis sem rolagem horizontal indevida | A preencher | Não executado |
| UX-03 | Navegar usando teclado | Campos e controles principais acessíveis por teclado e foco visível | A preencher | Não executado |
| UX-04 | Recarregar a página após uma abertura | Página volta a um estado utilizável; registrar se dados temporários são mantidos ou perdidos | A preencher | Não executado |

## 7. Registro de defeitos

Para cada falha, copie este modelo:

- **ID do teste:**
- **Data/hora:**
- **Ambiente e navegador:**
- **Passos para reproduzir:**
- **Resultado esperado:**
- **Resultado obtido:**
- **Frequência:** sempre / às vezes / uma vez
- **Evidência:** nome do arquivo de captura (sem dados pessoais)
- **Impacto:** bloqueador / alto / médio / baixo
- **Observação ou hipótese:** não confundir hipótese com causa confirmada.

## 8. Critérios para concluir a validação

- [ ] Fluxo de abertura testado de ponta a ponta.
- [ ] Validações do navegador e do webhook verificadas.
- [ ] Classificações e prioridades registradas com entradas variadas.
- [ ] Fallback da IA verificado em ambiente controlado.
- [ ] Persistência na planilha confirmada.
- [ ] E-mail de confirmação e alerta de prioridade alta conferidos.
- [ ] Chatbot testado com credenciais corretas e incorretas.
- [ ] Proteção contra consulta de chamados de terceiros verificada.
- [ ] Registro de informações adicionais confirmado.
- [ ] Falhas de integração verificadas ou explicitamente marcadas como não executadas.
- [ ] Teste em celular e computador realizado.
- [ ] Evidências revisadas para remover dados pessoais e segredos.

## 9. Observações técnicas encontradas na revisão documental

1. A árvore da branch `main` revisada nesta data contém `index.html`, `README.md` e arquivos em `docs/`, mas não apresenta a pasta `n8n/` citada na estrutura e no passo a passo do README. A documentação de configuração informa que o JSON de exportação não foi fornecido. Confirmar com o responsável se o workflow deve ser versionado ou se as instruções de importação devem ser removidas/ajustadas.
2. As URLs de demonstração citadas em diferentes documentos não são consistentes. Confirmar com o responsável qual é a URL oficial antes de padronizar a documentação.
3. O `index.html` consultado contém URLs de webhook no JavaScript. Endpoints públicos não são segredos; revisar proteção contra abuso, validação no servidor, CORS e monitoramento. Nunca inserir credenciais no frontend.
4. A documentação de configuração menciona uma URL de webhook diferente daquela encontrada no HTML. Confirmar a Production URL ativa diretamente no n8n antes de alterar qualquer endereço.

**Não corrigir endpoints nem publicar mudanças em workflows sem validar com o responsável pelo n8n.**
