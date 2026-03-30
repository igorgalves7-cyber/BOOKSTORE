Documente as respostas das seguintes questões no readme do nosso projeto: 
- Explique o conceito de Middleware no framework Express e por que ele é fundamental para processar requisições JSON vindas de um aplicativo mobile.

O middleware express.json() é vital para converter os dados brutos enviados por apps mobile em objetos JavaScript acessíveis via req.body. Sem ele, o servidor não "entende" o conteúdo da requisição.

- Quais são as principais diferenças entre um banco de dados NoSQL (orientado a documentos) e um banco SQL tradicional para um catálogo de livros que pode sofrer alterações constantes de estrutura?

SQL (Relacional): Possui estrutura rígida (tabelas e colunas fixas). Qualquer mudança exige alterações complexas no esquema do banco.

NoSQL (Documentos): Possui esquema dinâmico. É ideal para catálogos de livros onde novos campos (como "edição especial" ou "metadados técnicos") precisam ser adicionados rapidamente sem quebrar o sistema existente.

- Explique o papel do Hashing (via bcryptjs) e como ele protege os dados em caso de vazamento do banco.

Função: Transforma senhas em códigos irreversíveis (hashes) usando a técnica de salting (adição de caracteres aleatórios).

Segurança: Caso o banco de dados seja invadido, o invasor encontrará apenas os códigos criptografados. Como o processo é unidirecional, não é possível "descriptografar" o hash para descobrir a senha real do usuário.

- Qual a importância técnica e de segurança do arquivo .env e do pacote dotenv em um projeto que será compartilhado via GitHub ou implantado em produção?

Função: Armazena variáveis sensíveis (senhas de banco, chaves de API) fora do código-fonte.

Segurança: O arquivo .env deve ser listado no .gitignore para nunca ser enviado ao GitHub. O pacote dotenv garante que o sistema leia essas configurações localmente ou em produção sem expor dados críticos publicamente.