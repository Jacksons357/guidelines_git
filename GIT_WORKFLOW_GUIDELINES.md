# 📘 Git Workflow - Padrão de Colaboração

Este documento define o fluxo recomendado de trabalho com Git e as convenções de nomeação de branches, para manter o projeto organizado e facilitar a colaboração entre membros da equipe.

---

## ✅ Acessando uma branch existente (como `develop`)

1. **Verifique as branches existentes no repositório remoto:**

```bash
git fetch
git branch -r
```

2. **Acesse a branch remota `develop`:**

Se a branch `develop` ainda não está localmente:

```bash
git checkout -b develop origin/develop
```

Se ela já está localmente:

```bash
git checkout develop
```

3. **Atualize a branch:**

```bash
git pull origin develop
```

---

## 🧑‍💻 Criando uma nova branch para sua tarefa

Sempre crie uma nova branch a partir da `develop` (ou da branch que estiver sendo usada para desenvolvimento):

```bash
git checkout develop
git pull origin develop
git checkout -b tipo/nome-da-tarefa
```

---

## 🌱 Padrões de nomes de branch

Use o formato: `tipo/nome-da-tarefa`

| Tipo        | Descrição                                        | Exemplo                          |
|-------------|--------------------------------------------------|----------------------------------|
| `feature/`  | Nova funcionalidade                              | `feature/backend-api`            |
| `fix/`      | Correção de bug                                  | `fix/navbar-bug`                 |
| `hotfix/`   | Correção urgente em produção                     | `hotfix/deploy-crash`            |
| `refactor/` | Reestruturação de código (sem alterar comportamento) | `refactor/form-validation`    |
| `chore/`    | Tarefas administrativas (configs, dependências)  | `chore/update-dependencies`      |
| `test/`     | Adição ou melhoria de testes                     | `test/api-routes`                |
| `docs/`     | Atualização na documentação                      | `docs/add-readme`                |

> Use **kebab-case** para nomear tarefas: hífens em vez de espaços ou camelCase.

---

## 🔁 Fluxo completo de trabalho (Git Flow simplificado)

```bash
# 1. Acesse a branch de desenvolvimento
git checkout develop
git pull origin develop

# 2. Crie uma nova branch para sua tarefa
git checkout -b feature/nome-da-tarefa

# 3. Faça alterações, commits e push
git add .
git commit -m "feat: descreva sua mudança aqui"
git push origin feature/nome-da-tarefa

# 4. No GitHub, abra um Pull Request para a branch develop
```

---

## 🛑 Não comite diretamente na `main` ou `develop`

Sempre trabalhe em branches separadas e use **Pull Requests** para revisão e merge.

---

## ✅ Exemplo de commit

```bash
git commit -m "feat: cria rota de autenticação para login"
```

Use prefixos semânticos no commit:

- `feat:` → nova funcionalidade
- `fix:` → correção de bug
- `docs:` → documentação
- `refactor:` → refatoração
- `test:` → testes
- `chore:` → tarefas administrativas

---

## 🙌 Boas práticas

- Escreva mensagens de commit claras
- Sempre abra um Pull Request
- Aguarde revisão antes de dar merge
- Mantenha sua branch atualizada com `develop`

---
