# Casos de teste

Este documento separa resultados esperados do status registrado no material de desenvolvimento. Apenas o caso 1 estava marcado como aprovado com dados simulados na transcrição compartilhada. Os demais permanecem **pendentes de execução documentada** até que os testes sejam realizados e registrados.

| # | Cenário | Resultado esperado | Status conhecido |
|---:|---|---|---|
| 1 | "A internet caiu no setor inteiro" | Categoria Rede/Internet; prioridade Alta; alerta à equipe | Aprovado com dados simulados |
| 2 | "Esqueci minha senha do sistema" | Categoria Acesso/Senha; prioridade Média | Pendente |
| 3 | "Quero trocar o papel de parede" | Prioridade Baixa; sem alerta de urgência | Pendente |
| 4 | "Recebi um e-mail suspeito pedindo minha senha" | Prioridade Alta; orientar fluxo de segurança | Pendente |
| 5 | "Minha impressora não liga" | Categoria Hardware; prioridade Média | Pendente |
| 6 | E-mail inválido, por exemplo `maria@empresa` | Envio bloqueado com mensagem de validação | Pendente |
| 7 | Descrição com menos de 20 caracteres | Envio bloqueado com mensagem de validação | Pendente |
| 8 | Campos obrigatórios vazios | Página impede envio | Pendente |
| 9 | Descrição longa e caracteres especiais | Dados processados sem quebra de interface e sem injeção de HTML | Pendente |
| 10 | IA indisponível ou nó de IA desativado | Fallback; `classificado_por_ia = false`; fluxo continua | Pendente |
| 11 | Falha de Google Sheets ou credencial removida | Erro controlado; o sistema não deve fingir que o registro ocorreu | Pendente |

## Como executar os testes

1. Utilize ambiente de testes e dados inteiramente fictícios.
2. Registre data, entrada utilizada, resultado obtido e evidência (captura de tela sem credenciais ou dados pessoais).
3. Para cada teste, atualize o status para **Aprovado** ou **Falhou**, anotando eventuais diferenças em relação ao esperado.
4. Execute os testes de integração no workflow n8n, não apenas as validações do navegador.
5. Ao testar falhas, confirme a resposta HTTP e se o chamado ficou ou não registrado.

## Critérios gerais de aceite

- Dados inválidos não devem ser aceitos pelo backend.
- O resultado da IA precisa corresponder ao esquema e às categorias permitidas.
- O fallback precisa ser identificável, não pode mascarar falha de registro e deve permitir resposta controlada.
- Chamados classificados como Alta devem seguir a ramificação de alerta.
- A tela de confirmação só deve indicar sucesso de acordo com as garantias reais de persistência e notificação definidas pelo workflow.
