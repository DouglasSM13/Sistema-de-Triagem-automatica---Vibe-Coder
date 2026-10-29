# Configuração do workflow no n8n

Este documento descreve os componentes necessários para reproduzir ou revisar o workflow. O arquivo de exportação JSON do workflow não foi fornecido junto com os arquivos-fonte; por isso, esta documentação descreve o comportamento esperado, não substitui a inspeção dos nós no ambiente n8n.

## Visão geral

O workflow, chamado **Triagem Inteligente de Chamados de TI**, recebe dados por webhook, valida e normaliza os campos, gera protocolo, usa IA para classificar, registra o chamado e dispara notificações.

## Etapas

### 1. Entrada

- Criar um nó **Webhook** com método HTTP `POST`.
- Receber JSON com `nome`, `email`, `setor` e `descricao`.
- Configurar uma resposta JSON consistente para sucesso e erro.
- Como o formulário é servido em uma origem diferente do n8n, verificar CORS e preflight conforme a hospedagem escolhida.
- O endpoint de produção informado para esta instalação é `https://testes-udf-vibe-coding.app.n8n.cloud/webhook/abrir-chamado`. A URL foi inferida a partir do endereço de teste enviado (`/webhook-test/abrir-chamado`); confirme no próprio nó Webhook que a Production URL coincide e publique/ative o workflow. A URL de teste só funciona quando o n8n está ouvindo por um evento de teste. O endpoint não deve ser tratado como secreto ou mecanismo de autenticação.

### 2. Validação e normalização

Validar os dados no servidor, mesmo que a página também valide no navegador:

| Campo | Regra |
|---|---|
| `nome` | Obrigatório; pelo menos 3 caracteres após trim. |
| `email` | Obrigatório; validar formato e converter para minúsculas. |
| `setor` | Obrigatório; Financeiro, RH, Comercial, Operações ou Outro. |
| `descricao` | Obrigatória; no mínimo 20 caracteres após trim. |

Normalizar espaços externos antes do processamento. Em caso de validação falha, devolver erro estruturado e HTTP 422.

### 3. Protocolo

Gerar um identificador no formato `CH-AAAAMMDD-XXXX`, com a data de abertura e quatro caracteres aleatórios. Evitar caracteres ambíguos (por exemplo, O/0 e I/1). Para uso real, avaliar colisões e garantir unicidade no armazenamento.

### 4. Classificação com IA

Configuração descrita no protótipo:

- **Basic LLM Chain** com modelo OpenAI.
- Temperatura baixa (0,1) para reduzir variação.
- **Structured Output Parser** para solicitar uma saída JSON previsível.
- Campos de saída:
  - `categoria`: Hardware, Software, Rede/Internet, Acesso/Senha ou Outro.
  - `prioridade`: Baixa, Média ou Alta.
  - `resumo`: uma frase curta.
  - `sugestao_inicial`: orientação simples e segura.

Critérios sugeridos:

- **Alta:** afeta várias pessoas ou há possível incidente de segurança.
- **Média:** impede o trabalho de uma pessoa.
- **Baixa:** incômodo que não bloqueia o trabalho.

A IA auxilia na triagem, mas não deve substituir a avaliação humana, principalmente em incidentes de segurança.

### 5. Fallback

Se a chamada à IA falhar ou a resposta não puder ser interpretada, o workflow deve continuar com:

- `categoria = "Outro"`
- `prioridade = "Média"`
- `resumo`: primeiros 100 caracteres da descrição
- `sugestao_inicial = "Nossa equipe analisará seu chamado em breve."`
- `classificado_por_ia = false`

Registre esse estado no Sheets e informe a situação no retorno ao solicitante.

### 6. Google Sheets

Criar uma planilha com as colunas, na ordem esperada:

`protocolo, data_abertura, nome, email, setor, descricao, categoria, prioridade, resumo, classificado_por_ia, status`

O status inicial é `Aberto`. Restringir o compartilhamento da planilha e evitar dados reais em demonstrações.

### 7. E-mail e ramificação por prioridade

- Enviar ao solicitante uma confirmação com protocolo, categoria, prioridade, resumo e sugestão inicial.
- Ramificar pela prioridade.
- Se a prioridade for `Alta`, enviar aviso à equipe de suporte com assunto no formato `[URGENTE] Novo chamado <protocolo>`.
- Definir e testar o tratamento de falhas de Sheets e Gmail; não declarar sucesso se o registro não tiver ocorrido.

### 8. Resposta para o frontend

O frontend espera um objeto JSON de sucesso com `sucesso: true`, protocolo e dados de triagem. A resposta de fallback deve permitir ao cliente exibir que a IA não conseguiu classificar. Para erros de validação, devolver HTTP 422 com uma estrutura que a página consiga apresentar.

## Credenciais e segurança

- Configure credenciais do Google, Gmail e provedor de IA no gerenciador de credenciais do n8n.
- Não coloque chaves, tokens, senhas ou credenciais no HTML, no repositório ou nos prompts.
- Restrinja a exposição do webhook com controles apropriados para o cenário de uso; avalie limitação de requisições, proteção contra spam e monitoramento.
- Revise uma exportação do workflow antes de publicá-la, removendo IDs internos e dados específicos do ambiente.

## Checklist antes de demonstrar

- [ ] Credenciais funcionais configuradas no n8n.
- [ ] Validação executada também no servidor.
- [ ] Resposta HTTP 422 testada.
- [ ] Saída válida da IA conferida.
- [ ] Fallback da IA testado.
- [ ] Gravação no Sheets conferida.
- [ ] E-mail de confirmação conferido.
- [ ] Alerta de prioridade alta conferido.
- [ ] Falhas das integrações testadas.
- [ ] Página configurada com a URL correta de webhook.
- [ ] Apenas dados fictícios utilizados na demonstração.
