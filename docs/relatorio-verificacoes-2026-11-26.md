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
| V-05 | Documental | Link para export do chatbot | Divergência: README aponta para arquivo ausente na árvore de `main`. |
| V-06 | Documental | URL da demonstração | Divergência: README apresenta dois domínios Vercel. |
| V-07 | Documental | URL de webhook | Divergência entre host no HTML e host citado em `docs/configuracao-n8n.md`. |
| V-08 | Execução relatada | Abertura de chamado compartilhada em 26/11 | Sucesso relatado; categoria Software, prioridade Média e protocolo gerado (mascarado no registro público). |
| V-09 | Integração | Conferência direta da planilha | Não verificada nesta revisão. |
| V-10 | Integração | Entrega efetiva do e-mail | Conteúdo compartilhado pelo testador; entrega na caixa de entrada não verificada independentemente. |
| V-11 | Execução externa | Teste POST dos webhooks | Não executado: requer ambiente autorizado e dados de teste; não enviar requisições de teste não combinadas à produção. |
| V-12 | Segurança | Chat com e-mail incorreto | Não verificado no workflow n8n. |
| V-13 | Resiliência | Fallback de IA e falhas Sheets/Gmail | Não verificado no workflow n8n. |

## Registro da abertura compartilhada

- Data/hora exibida: 26/11/2026, 09:49:35.
- Descrição: usuário impossibilitado de realizar a saída de produtos no sistema de coleta.
- Categoria retornada: Software.
- Prioridade retornada: Média.
- Resumo retornado: coerente com a descrição.
- Confirmação na página: exibida.
- Conteúdo da confirmação por e-mail: compartilhado pelo testador.
- Dados identificadores: omitidos.

## Como interpretar

“Concluída” nas verificações estáticas significa que o trecho foi localizado no código; não significa que o serviço externo respondeu. “Sucesso relatado” indica evidência fornecida pelo testador, sem inspeção independente da infraestrutura. “Não verificado” não significa falha: significa ausência de evidência nesta revisão.
