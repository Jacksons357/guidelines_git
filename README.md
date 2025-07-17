# 📘 Git Workflow - Padrão de Colaboração

Este documento define o fluxo recomendado de trabalho com Git e as convenções de nomeação de branches, para manter o projeto organizado e facilitar a colaboração entre membros da equipe.

---

## 🚀 Primeiros passos (Configuração inicial)

###1. Configurar Git (apenas na primeira vez)

```bash
git config --global user.name "Seu Nome"
git config --global user.email seu.email@exemplo.com
```

### 2. Clonar o repositório (primeira vez no projeto)

```bash
git clone https://github.com/usuario/nome-do-repositorio.git
cd nome-do-repositorio
```

### 3. Verificar status e configurações

```bash
git status                    # Ver arquivos modificados
git remote -v                 # Ver repositórios remotos
git branch -a                 # Ver todas as branches (locais e remotas)
```

---

## ✅ Acessando uma branch existente (como `develop`)1ize as informações do repositório remoto:**

```bash
git fetch origin
```
2ifique as branches existentes:**

```bash
git branch -r                  # Branches remotas
git branch -a                  # Todas as branches (locais e remotas)
```

3. **Acesse a branch `develop`:**

Se a branch `develop` ainda não está localmente:

```bash
git checkout -b develop origin/develop
```

Se ela já está localmente:

```bash
git checkout develop
```

4. **Atualize a branch com as últimas mudanças:**

```bash
git pull origin develop
```

---

## 🧑‍💻 Criando uma nova branch para sua tarefa

Sempre crie uma nova branch a partir da `develop` (ou da branch que estiver sendo usada para desenvolvimento):

```bash
# 1. Certifique-se de estar na branch de desenvolvimento
git checkout develop

# 2tualize com as últimas mudanças
git pull origin develop

# 3. Crie e acesse sua nova branch
git checkout -b tipo/nome-da-tarefa
```

**Comando alternativo (mais moderno):**
```bash
git switch -c tipo/nome-da-tarefa
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
| `style/`    | Alterações de formatação (espaços, ponto e vírgula) | `style/fix-indentation`      |
| `perf/`     | Melhorias de performance                         | `perf/optimize-database-query`   |

> Use **kebab-case** para nomear tarefas: hífens em vez de espaços ou camelCase.

---

## 🔁 Fluxo completo de trabalho (Git Flow simplificado)

```bash
# 1Acesse a branch de desenvolvimento
git checkout develop
git pull origin develop

# 2. Crie uma nova branch para sua tarefa
git checkout -b feature/nome-da-tarefa

# 3ça suas alterações no código
# ... edite os arquivos ...

# 4. Verifique o status das alterações
git status
git diff

# 5. Adicione as alterações ao staging
git add .                      # Adiciona todos os arquivos
# OU
git add arquivo-especifico.js  # Adiciona arquivo específico

# 6. Faça o commit com mensagem descritiva
git commit -m "feat: descreva sua mudança aqui
# 7vie para o repositório remoto
git push origin feature/nome-da-tarefa

# 8No GitHub, abra um Pull Request para a branch develop
```

---

## 📝 Trabalhando com commits

### Estrutura de mensagens de commit

Use o formato: `tipo: descrição curta`

```bash
git commit -m "feat: adiciona sistema de autenticação"
git commit -mfix: corrige bug no formulário de login"
git commit -m "docs: atualiza README com instruções de instalação"
```

### Prefixos semânticos

- `feat:` → nova funcionalidade
- `fix:` → correção de bug
- `docs:` → documentação
- `refactor:` → refatoração
- `test:` → testes
- `chore:` → tarefas administrativas
- `style:` → formatação de código
- `perf:` → melhorias de performance
- `ci:` → configurações de CI/CD
- `build:` → alterações no build

### Commit com descrição detalhada

```bash
git commit -m "feat: adiciona sistema de autenticação

- Implementa login com email e senha
- Adiciona validação de formulário
- Cria middleware de autenticação
- Adiciona testes unitários"
```

---

## 🔄 Mantendo sua branch atualizada

### Atualizar sua branch com `develop`

```bash
# Opção 1: Merge (mantém histórico linear)
git checkout feature/sua-branch
git fetch origin
git merge origin/develop

# Opção 2: Rebase (histórico mais limpo)
git checkout feature/sua-branch
git fetch origin
git rebase origin/develop
```

### Resolver conflitos

Se houver conflitos durante merge/rebase:
1 **Git mostrará os arquivos com conflitos**
2*Edite os arquivos manualmente** (procure por `<<<<<<<`, `=======`, `>>>>>>>`)
3. **Adicione os arquivos resolvidos:**
   ```bash
   git add arquivo-com-conflito.js
   ```
4. **Continue o processo:**
   ```bash
   git rebase --continue  # se estava fazendo rebase
   # OU
   git merge --continue   # se estava fazendo merge
   ```

---

## 🛑 Regras importantes

### ❌ NUNCA faça isso:
- Comitar diretamente na `main` ou `develop`
- Fazer push de código não testado
- Usar mensagens de commit vagas como fix ou update- Deletar branches de outros desenvolvedores

### ✅ SEMPRE faça isso:
- Trabalhe em branches separadas
- Use Pull Requests para revisão
- Escreva mensagens de commit claras
- Teste seu código antes do commit
- Mantenha sua branch atualizada

---

## 🔧 Comandos úteis para o dia a dia

### Verificar histórico
```bash
git log --oneline -10         # Últimos 10commits
git log --graph --oneline      # Histórico com gráfico
git show <commit-hash>         # Detalhes de um commit
```

### Gerenciar branches
```bash
git branch                      # Lista branches locais
git branch -d nome-branch       # Deleta branch local
git branch -D nome-branch       # Força deleção de branch
git push origin --delete nome-branch  # Deleta branch remota
```

### Desfazer alterações
```bash
git checkout -- arquivo.js      # Desfaz alterações em arquivo
git reset --hard HEAD~1   # Desfaz último commit
git revert <commit-hash>        # Cria commit que desfaz outro
```

### Stash (salvar alterações temporariamente)
```bash
git stash                       # Salva alterações temporariamente
git stash pop                   # Restaura alterações salvas
git stash list                  # Lista stashes salvos
```

---

## 🙌 Boas práticas

- ✅ Escreva mensagens de commit claras e descritivas
- ✅ Sempre abra um Pull Request para revisão
- ✅ Aguarde aprovação antes de fazer merge
- ✅ Mantenha sua branch atualizada com `develop`
- ✅ Teste seu código antes de commitar
- ✅ Use branches descritivas e organizadas
- ✅ Revise o código de outros desenvolvedores
- ✅ Documente mudanças importantes
- ✅ Use tags para releases importantes

---

## 🆘 Solução de problemas comuns

### Branch divergiu do remote
```bash
git pull --rebase origin develop
```

### Commit no branch errado
```bash
git reset --soft HEAD~1   # Remove commit mantendo alterações
git checkout branch-correta
git commit -m "sua mensagem
```
### Arquivo deletado acidentalmente
```bash
git checkout HEAD -- arquivo.js
```

### Ver diferenças entre branches
```bash
git diff develop..feature/sua-branch
```

---

## 📚 Recursos adicionais

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
