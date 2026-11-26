# Relatório de verificações executadas

**Data:** 26/11/2026  
**Escopo:** leitura estática dos arquivos do repositório e registro de uma execução real compartilhada pelo contribuinte.

## Resultado resumido

| ID | Tipo | Verificação | Resultado |
|---|---|---|---|
| V-01 | Estática | Presença das constantes de webhook no HTML | Concluída: abertura e chat apontam para o host `udf-tendencias-ccp.app.n8n.cloud`. |
| V-02 | Estática | Regras de validação do formulário | Concluída: nome >= 3, e-mail validado por expressão regular, setor obrigatório e descrição >= 20. |
| V-03 | Estática | Tratamento de sucesso/erro no frontend | Concluída: sucesso depende de `r.corpo.sucesso === true`; há tratamento de HTTP 422. |
| V-04 | Estática | Dados enviados ao chatbot | Concluída: protocolo, e-mail, sessionId e mensagem. A autorização no backend não foi verificada. |
| V-05 | Documental | Export do chatbot | Pendente: o README foi corrigido para não prometer um JSON importável; o arquivo `n8n/chatbot-chamados-n8n.json` não está presente na árvore consultada de `main`. |
| V-06 | Documental | URL da demonstração | Resolvida: README padronizado para `https://sistema-de-triagem-automatica.vercel.app/`, endereço confirmado pelo responsável pelo teste. |
| V-07 | Documental | URL de webhook | Resolvida quanto ao texto: `docs/configuracao-n8n.md` e frontend usam o host `udf-tendencias-ccp.app.n8n.cloud`; estado ativo no painel n8n não inspecionado. |
| V-08 | Execução relatada | Primeira abertura em 26/11 | Sucesso relatado; categoria Software, prioridade Média e sugestão inicial exibida. |
| V-09 | Integração | Conferência direta da planilha | Não verificada nesta revisão. |
| V-10 | Integração | E-mail da segunda execução | Recebimento na caixa de entrada confirmado pelo testador para o chamado `CH-20261126-VCTH`. |
| V-11 | Execução externa | Teste POST dos webhooks | Não executado: requer ambiente autorizado e dados de teste; não enviar requisições de teste não combinadas à produção. |
| V-12 | Segurança | Chat com e-mail incorreto | Não verificado no workflow n8n. |
| V-13 | Resiliência | Fallback de IA e falhas Sheets/Gmail | Não verificado no workflow n8n. |
| V-14 | Execução relatada | Segunda abertura, consulta pelo chatbot e e-mail em 26/11 | Sucesso relatado pelo testador: protocolo `CH-20261126-VCTH`, Rede/Internet, Alta; chatbot respondeu status `Aberto`; e-mail recebido. Persistência no Sheets e alerta interno não verificados. |

## Registros das execuções compartilhadas

### Primeira execução

- Data/hora exibida: 26/11/2026, 09:49:35.
- Descrição: usuário impossibilitado de realizar a saída de produtos no sistema de coleta.
- Categoria retornada: Software.
- Prioridade retornada: Média.
- Resumo e sugestão inicial: exibidos na página.
- Dados identificadores: omitidos.

### Segunda execução

- Data: 26/11/2026.
- Protocolo: `CH-20261126-VCTH`.
- Cenário: instabilidade ou queda de conexão de internet afetando todo o setor.
- Categoria: Rede/Internet; prioridade: Alta.
- Página: confirmação e sugestão inicial exibidas.
- Chatbot: respondeu à pergunta sobre andamento com status `Aberto`.
- Gmail: o testador confirmou o recebimento do e-mail de confirmação na caixa de entrada.
- Não verificados independentemente: gravação no Google Sheets e alerta interno para a equipe.
- Dados pessoais: omitidos.

## Como interpretar

“Concluída” nas verificações estáticas significa que o trecho foi localizado no código; não significa que o serviço externo respondeu. “Sucesso relatado” indica evidência fornecida pelo testador, sem inspeção independente da infraestrutura. “Não verificado” não significa falha: significa ausência de evidência nesta revisão.
