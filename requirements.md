# BiblioShare API (Empréstimo de Livros)

**Foco:** Relacionamento de tabelas e status booleano.

## 1. Acervo

* **RF01 - Cadastro de Livros:** Cadastrar livros com título, autor e ano. O livro deve ser criado, por padrão, com o status de *Disponível* (ou campo `membro_id` vazio/null).
* **RF02 - Cadastro de Membros:** Cadastrar usuários da biblioteca (nome, telefone).
* **RF03 - Busca Inteligente:** Rota para buscar livros por título ou autor.

## 2. Circulação (O Core)

* **RF04 - Realizar Empréstimo:** Rota que recebe `id_livro` e `id_membro`.
    > **Regra de Ouro:** A API deve verificar se o livro já possui um `membro_id` vinculado.
    > * **Se sim:** Retornar erro informando que o livro já está emprestado.
    > * **Se não:** Vincular o ID do membro ao livro.
* **RF05 - Devolução:** Rota que recebe o `id_livro`. Ela deve remover o vínculo com o membro (setar `membro_id` para `null`), tornando o livro disponível novamente na busca.
* **RF06 - Meus Empréstimos:** Rota que lista todos os livros que estão atualmente na posse de um membro específico.
