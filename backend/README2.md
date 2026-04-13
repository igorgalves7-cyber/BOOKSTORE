#  Validação de Dados com Postman: A Primeira Linha de Defesa

Este documento descreve a importância estratégica de configurar **Constraints** (restrições) e **Tipos de Dados** no Postman para garantir a estabilidade de aplicações móveis, especificamente em **React Native**.

---

##  Visão Geral

No desenvolvimento Full Stack, o **Postman** atua como o "porteiro" da infraestrutura. Antes de um dado chegar à interface do utilizador no React Native, ele deve ser validado pela API. Se a API enviar informações inconsistentes, o aplicativo móvel pode sofrer *crashes* ou comportamentos imprevistos.



---

##  1. O Papel dos Tipos de Dados

Os tipos de dados definem a natureza da informação (String, Number, Boolean, Object, Array). No Postman, a validação de tipos garante o "contrato" entre o Back-end e o Front-end.

* **Prevenção de Erros de Tipagem:** Se o React Native espera um `number` para realizar um cálculo de preço e recebe uma `string` (ex: `"10.50"` em vez de `10.50`), a aplicação pode falhar ou exibir `NaN`.
* **Consistência de Estrutura:** Garante que listas (Arrays) e objetos cheguem no formato exato que os componentes do React Native (como `FlatList`) esperam para renderizar.

---

##  2. Constraints (Restrições) como Regras de Negócio

As *Constraints* são validações lógicas que vão além do tipo de dado. Elas impedem que dados "anormais" quebrem a lógica do app.

### Exemplos Práticos:

| Restrição | Exemplo de Erro Evitado | Impacto no React Native |
| :--- | :--- | :--- |
| **Minimum / Maximum** | Idade negativa (ex: -5) | Evita erros em cálculos de data e lógica de permissões. |
| **Format (Email/UUID)** | E-mail sem "@" ou domínio | Impede falhas em fluxos de autenticação e comunicação. |
| **Unique Items** | IDs duplicados num Array | Evita erros de "Duplicate Keys" ao renderizar listas. |
| **Required Fields** | Campo `token` ausente | Previne o erro fatal: `Cannot read property of undefined`. |

---

##  3. Postman como "Primeira Linha de Teste"

A configuração de testes automatizados no Postman permite que os erros sejam detetados **antes** de o código ser integrado no ambiente mobile.

### Como funciona o fluxo:
1.  **Execução do Request:** O Postman chama o endpoint da API.
2.  **Validação de Schema:** Através da aba *Tests*, verifica-se se o JSON retornado respeita as regras (JSON Schema).
3.  **Feedback Imediato:** Se um desenvolvedor de Back-end alterar um campo ou remover uma restrição, o teste falha instantaneamente, alertando a equipa antes que o erro chegue ao utilizador final.



---

##  Exemplo de Implementação (Postman Script)

Podes utilizar o seguinte script na aba **Tests** do Postman para validar um perfil de utilizador:

```javascript
// Definição do Schema (Contrato)
const schema = {
    "type": "object",
    "required": ["id", "nome", "idade", "email"],
    "properties": {
        "id": { "type": "string", "format": "uuid" },
        "nome": { "type": "string", "minLength": 2 },
        "idade": { "type": "number", "minimum": 18, "maximum": 120 },
        "email": { "type": "string", "format": "email" }
    }
};

// Teste de Integridade
pm.test("Validar se os dados são seguros para o React Native", function () {
    pm.response.to.have.jsonSchema(schema);
});