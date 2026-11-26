# Casos de teste

Este documento separa resultados esperados de evidências efetivamente relatadas. O caso 1 abaixo já constava como aprovado com dados simulados no material de desenvolvimento. Em 26/11/2026 foram relatadas duas execuções manuais: a primeira de abertura de chamado (caso 12) e a segunda com abertura, consulta pelo chatbot e recebimento do e-mail (caso 13). Após as execuções, Douglas confirmou ao responsável pelo registro que a persistência no Google Sheets, o alerta interno para prioridade Alta e os workflows no n8n estão funcionando. Trata-se de confirmação do mantenedor repassada por Nathan, não de inspeção independente desta revisão. A exportação e o versionamento dos workflows JSON ainda não foram comprovados na árvore do Git. Os demais cenários permanecem **pendentes de execução documentada**.

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
| 12 | Abertura manual em 26/11/2026: chamado sobre impossibilidade de saída de produtos no sistema de coleta | Página exibe confirmação, protocolo mascarado, categoria Software, prioridade Média e sugestão inicial | Executado pelo usuário; evidência inicial registrada |
| 13 | Abertura e acompanhamento em 26/11/2026: instabilidade de internet afetando todo o setor | Protocolo `CH-20261126-VCTH`, categoria Rede/Internet, prioridade Alta, sugestão inicial; chatbot consulta o status Aberto; e-mail de confirmação chega à caixa de entrada | Executado pelo usuário; página, chatbot e e-mail confirmados; gravação no Sheets e alerta interno não verificados independentemente |

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
