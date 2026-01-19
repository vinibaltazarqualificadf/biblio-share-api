### BiblioShare API (Empréstimo de Livros)

**Cenário:** Uma biblioteca comunitária onde é preciso controlar quem está com qual livro.
**Desafio de Lógica:** Controle de Disponibilidade (Status).

#### 🗄️ Entidades (Banco de Dados)
* **Membros:** `id`, `nome`, `telefone`.
* **Livros (Simplificação):** `id`, `titulo`, `autor`, `membro_id` (FK - pode ser `NULL`).
    * *Nota: Nesta simplificação, o livro recebe diretamente o ID do membro que o pegou.*

#### 🔌 Requisitos Funcionais (Endpoints)

* `POST /livros`
    * Cadastrar livros novos.

* `PATCH /emprestar`
    * Recebe `livro_id` e `membro_id`.
    * **Regra de Ouro:** Só pode emprestar se o campo `membro_id` do livro estiver vazio (`NULL`). Se já tiver alguém, retornar erro `400`.

* `PATCH /devolver`
    * Recebe `livro_id`.
    * Limpa o campo `membro_id` (torna `NULL` novamente), deixando o livro disponível.

* `GET /livros/disponiveis`
    * Lista apenas livros que não estão com ninguém (onde `membro_id` é `NULL`).

* `GET /membros/<id>/historico`
    * Mostra quais livros estão atualmente com aquele membro.
