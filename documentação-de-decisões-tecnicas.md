# 🛠️ Documentação de Decisões Técnicas

## 1. **Ações e Decisões tomadas**

### **1.1. Desagrupamento de Cargas (Split Out)**

* **Desafio:** O webhook do n8n recebe todos os clientes agrupados em uma única lista (`body.clientes`).

* **Decisão:** Utilização do nó **Split Out (Item Lists)** para desmembrar a requisição em itens individuais no n8n, garantindo que as operações subsequentes ocorram por cliente.

### **1.2. Cruzamento de Perfis**

* **Desafio:** A base de dados de investimentos (`data.csv`) possui múltiplas opções por perfil (ex: 3 opções para perfil "Conservador"). O nó de Merge por padrão gerava triplicações para cada cliente.

* **Decisão:** Implementação de filtragem via **JavaScript Code** utilizando a estrutura de dados `Set` (`clientesVistos`). O código processa e valida apenas a primeira ocorrência do cliente (por e-mail/nome), garantindo a geração de exatamente **uma mensagem por cliente**.

### **2. Estrutura do Prompt de IA**

O prompt foi refinado com regras estritas:

* Formatação obrigatória em JSON com os campos `subject`, `text_body` e `html_body`.

* Proibição expressa de marcações markdown (```` ```json ````) para evitar falhas no parse.

* Instruções claras de empatia e limitação a apenas um parágrafo por recomendação.