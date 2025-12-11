# 🚀 Guia Completo de Git e GitHub

> Uma referência completa e prática para dominar o versionamento de código com Git

![Git & GitHub](https://hermes.dio.me/articles/cover/e34ac480-ce44-439a-b28b-1845bd195afe.png#vitrinedev)

## 📋 Índice

| Seção | Descrição | Link |
|-------|-----------|------|
| 🔧 | Configuração Inicial | [Ver comandos](#-configuração-inicial) |
| 🎯 | Comandos Essenciais | [Ver comandos](#-comandos-essenciais) |
| 🌿 | Branches | [Ver comandos](#-branches) |
| 🔄 | Sincronização | [Ver comandos](#-sincronização) |
| 🏷️ | Tags e Releases | [Ver comandos](#️-tags-e-releases) |
| 📝 | Histórico e Logs | [Ver comandos](#-histórico-e-logs) |
| 🔀 | Merge e Rebase | [Ver comandos](#-merge-e-rebase) |
| 🎯 | Múltiplos Remotos | [Ver comandos](#-múltiplos-repositórios-remotos) |
| 💡 | Dicas Avançadas | [Ver comandos](#-dicas-avançadas) |
| 🆘 | Solução de Problemas | [Ver comandos](#-solução-de-problemas) |

---

## 🔧 Configuração Inicial

### Configurações Globais
```bash
# Configurações básicas do usuário
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"

# Configurações úteis
git config --global init.defaultBranch main              # Define branch padrão como 'main'
git config --global core.editor "code --wait"            # Define VS Code como editor padrão
git config --global color.ui auto                        # Habilita cores no terminal
git config --global core.autocrlf true                   # Corrige problemas de quebra de linha (Windows)
git config --global core.longpaths true                  # Permite caminhos longos (Windows)
git config --global pull.rebase false                    # Define merge como padrão no pull

# Verificar configurações
git config --list                                        # Lista todas as configurações
git config user.name                                     # Verifica uma configuração específica
```

---

## 🎯 Comandos Essenciais

### Inicializando um Repositório
```bash
# Criar novo repositório
git init                                          # Inicializa repositório local
git init {nome-da-pasta}                          # Cria pasta e inicializa repositório

# Clonar repositório existente
git clone {url-do-repositório}                    # Clona repositório completo
git clone {url} {nome-pasta}                      # Clona com nome personalizado
git clone --depth 1 {url}                         # Clona apenas último commit (shallow clone)
git clone -b {branch} --single-branch {url}       # Clona apenas uma branch específica
```

### Trabalhando com Arquivos
```bash
# Adicionar arquivos
git add {arquivo}                                 # Adiciona arquivo específico
git add .                                         # Adiciona todos os arquivos modificados
git add *.{extensão}                              # Adiciona arquivos por extensão
git add -p                                        # Adiciona mudanças interativamente

# Remover arquivos
git rm {arquivo}                                  # Remove arquivo do repositório e do disco
git rm --cached {arquivo}                         # Remove apenas do repositório (mantém no disco)
git rm -r --cached {pasta}                        # Remove pasta do repositório

# Mover/Renomear arquivos
git mv {arquivo-antigo} {arquivo-novo}            # Renomeia ou move arquivo
```

### Commits
```bash
# Criar commits
git commit -m "Mensagem do commit"                # Commit com mensagem
git commit -am "Mensagem"                         # Add + Commit (apenas arquivos rastreados)
git commit --amend -m "Nova mensagem"             # Altera último commit
git commit --amend --no-edit                      # Adiciona mudanças ao último commit

# Desfazer commits
git reset HEAD~1                                  # Desfaz último commit (mantém mudanças)
git reset --soft HEAD~1                           # Desfaz commit (mantém mudanças staged)
git reset --hard HEAD~1                           # Desfaz commit (descarta mudanças)
git revert {hash-commit}                          # Cria novo commit revertendo mudanças
```

### Arquivo .gitignore
```bash
# Criar arquivo .gitignore
touch .gitignore                                  # Cria arquivo (Linux/Mac/Git Bash)
echo > .gitignore                                 # Cria arquivo
echo "Arquivo/Pasta" >> .gitignore                # Cria o arquivo com texto

# Padrões comuns do .gitignore
*.log                                             # Ignora todos os arquivos .log
/node_modules                                     # Ignora pasta node_modules na raiz
**/.env                                           # Ignora .env em qualquer pasta
!importante.log                                   # Não ignora arquivo específico
temp/                                             # Ignora pasta temp
*.{jpg,png,gif}                                   # Ignora múltiplas extensões

# Ignorar arquivo já rastreado
git rm --cached {arquivo}                         # Remove do rastreamento
git add .gitignore                                # Adiciona regra ao .gitignore
git commit -m "Ignorando arquivo"                 # Confirma mudanças
```

---

## 🌿 Branches

### Gerenciamento de Branches
```bash
# Listar branches
git branch                                        # Lista branches locais
git branch -r                                     # Lista branches remotas
git branch -a                                     # Lista todas as branches
git branch -v                                     # Lista branches com último commit
git branch --merged                               # Lista branches já mergeadas
git branch --no-merged                            # Lista branches não mergeadas

# Criar e alternar branches
git branch {nome-branch}                          # Cria nova branch
git checkout {nome-branch}                        # Alterna para branch
git checkout -b {nome-branch}                     # Cria e alterna para nova branch
git switch {nome-branch}                          # Alterna branch (Git 2.23+)
git switch -c {nome-branch}                       # Cria e alterna (Git 2.23+)

# Renomear e deletar branches
git branch -m {novo-nome}                         # Renomeia branch atual
git branch -m {nome-antigo} {nome-novo}           # Renomeia branch específica
git branch -d {nome-branch}                       # Deleta branch (safe)
git branch -D {nome-branch}                       # Força deleção de branch
git push origin --delete {nome-branch}            # Deleta branch remota
```

### Comparando Branches
```bash
git diff {branch1} {branch2}                      # Compara duas branches
git diff {branch1}...{branch2}                    # Compara desde o ancestral comum
git log {branch1}..{branch2}                      # Commits em branch2 que não estão em branch1
git show-branch {branch1} {branch2}               # Visualiza histórico das branches
```

---

## 🔄 Sincronização

### Trabalhando com Remotos
```bash
# Gerenciar remotos
git remote -v                                     # Lista remotos configurados
git remote add origin {url}                       # Adiciona remoto principal
git remote add {nome} {url}                       # Adiciona remoto adicional
git remote rename {nome-antigo} {nome-novo}       # Renomeia remoto
git remote remove {nome}                          # Remove remoto
git remote set-url origin {nova-url}              # Altera URL do remoto
git remote show origin                            # Mostra informações do remoto

# Push (Enviar mudanças)
git push origin {branch}                          # Envia branch para remoto
git push -u origin {branch}                       # Envia e configura upstream
git push --all origin                             # Envia todas as branches
git push --tags                                   # Envia todas as tags
git push --force                                  # Força envio (CUIDADO!)
git push --force-with-lease                       # Força envio seguro

# Pull e Fetch (Receber mudanças)
git fetch                                         # Baixa mudanças sem aplicar
git fetch --all                                   # Baixa de todos os remotos
git fetch --prune                                 # Remove referências obsoletas
git pull                                          # Baixa e aplica mudanças
git pull --rebase                                 # Pull com rebase ao invés de merge
git pull origin {branch}                          # Pull de branch específica
```

---

## 🏷️ Tags e Releases

### Trabalhando com Tags
```bash
# Listar e visualizar tags
git tag                                           # Lista todas as tags
git tag -l "v1.8*"                                # Lista tags com padrão
git show {nome-tag}                               # Mostra informações da tag

# Criar tags
git tag {nome-tag}                                # Cria tag leve
git tag -a {nome-tag} -m "Mensagem"               # Cria tag anotada
git tag -a {nome-tag} {hash-commit}               # Tag em commit específico
git tag -s {nome-tag} -m "Mensagem"               # Tag assinada com GPG

# Gerenciar tags
git tag -d {nome-tag}                             # Deleta tag local
git push origin --delete {nome-tag}               # Deleta tag remota
git push origin {nome-tag}                        # Envia tag específica
git push --tags                                   # Envia todas as tags
git checkout {nome-tag}                           # Navega para tag
```

---

## 🔀 Merge e Rebase

### Merge
```bash
# Merge básico
git merge {branch}                                # Merge de branch
git merge --no-ff {branch}                        # Força criação de commit de merge
git merge --ff-only {branch}                      # Apenas fast-forward
git merge --abort                                 # Cancela merge em andamento

# Resolver conflitos
git status                                        # Verifica arquivos em conflito
git diff                                          # Visualiza conflitos
git add {arquivo-resolvido}                       # Marca como resolvido
git merge --continue                              # Continua após resolver conflitos
```

### Rebase
```bash
# Rebase básico
git rebase {branch}                               # Rebase em cima de branch
git rebase -i HEAD~3                              # Rebase interativo dos últimos 3 commits
git rebase --onto {nova-base} {antiga-base}       # Rebase avançado
git rebase --abort                                # Cancela rebase
git rebase --continue                             # Continua após resolver conflitos
git rebase --skip                                 # Pula commit problemático

# Comandos no rebase interativo
# pick = usar commit
# reword = usar commit, mas editar mensagem
# edit = usar commit, mas parar para alterações
# squash = usar commit, mas juntar com anterior
# fixup = como squash, mas descarta mensagem
# drop = remove commit
```

---

## 🎯 Múltiplos Repositórios Remotos

### Caso de Uso: Repositório Público e Privado

Imagine que você tem um projeto onde parte do código é pública e parte é privada. Você quer manter um repositório privado com TUDO e um público apenas com o código que pode ser compartilhado.

#### Configuração Completa Passo a Passo
```bash
# 1. CRIAR O PROJETO E CONFIGURAR REMOTOS
mkdir meu-projeto && cd meu-projeto
git init

# Adicionar os dois repositórios remotos
git remote add privado https://github.com/usuario/repo-privado.git
git remote add publico https://github.com/usuario/repo-publico.git

# Verificar se está tudo certo
git remote -v
# Deve mostrar:
# privado  https://github.com/usuario/repo-privado.git (fetch)
# privado  https://github.com/usuario/repo-privado.git (push)
# publico  https://github.com/usuario/repo-publico.git (fetch)
# publico  https://github.com/usuario/repo-publico.git (push)

# 2. CRIAR OS ARQUIVOS DO PROJETO
echo "Código público" > arquivo-publico.js
echo "Código privado com segredos" > arquivo-privado.js  
echo "API_KEY=secret123" > .env
echo "Documentação pública" > README.md

# 3. CRIAR BRANCH PRIVADA (com TODOS os arquivos)
git add .                                         # Adiciona TODOS os 4 arquivos
git commit -m "Versão completa do projeto"
git branch -M main-privado                        # Renomeia a branch para main-privado

# Neste ponto você tem:
# Branch: main-privado com 4 arquivos (publico.js, privado.js, .env, README.md)

# 4. CRIAR BRANCH PÚBLICA (removendo arquivos sensíveis)
git checkout -b main-publico                      # Cria NOVA branch baseada na privada
git rm arquivo-privado.js .env                    # Remove os arquivos sensíveis
git commit -m "Remove arquivos privados"          # Salva a remoção

# Agora você tem:
# Branch: main-publico com 2 arquivos (publico.js, README.md)

# 5. ENVIAR CADA BRANCH PARA SEU REPOSITÓRIO
git push privado main-privado:main                # Envia branch privada → repo privado
git push publico main-publico:main                # Envia branch pública → repo público
```

#### Automatizando com Alias
```bash
# Criar comandos personalizados para facilitar
git config --global alias.sync-public '!git checkout main-publico && git cherry-pick main-privado && git push publico main-publico:main && git checkout main-privado'

# Agora você pode sincronizar com um comando só:
git sync-public
```

---

## 🆘 Solução de Problemas

### Desfazer Mudanças
```bash
# Desfazer mudanças não commitadas
git checkout -- {arquivo}                         # Descarta mudanças em arquivo
git checkout .                                    # Descarta todas as mudanças
git restore {arquivo}                             # Restaura arquivo (Git 2.23+)
git restore --staged {arquivo}                    # Remove do stage
git clean -df                                     # Remove arquivos não rastreados

# Recuperar commits perdidos
git reflog                                        # Visualiza histórico de referências
git checkout {hash-reflog}                        # Recupera commit
git reset --hard {hash-reflog}                    # Restaura para estado anterior
```

### Corrigir Problemas Comuns
```bash
# Corrigir último commit
git commit --amend                                # Abre editor para alterar
git commit --amend --no-edit                      # Adiciona mudanças sem editar mensagem
git commit --amend --author="Nome <email>"        # Altera autor
```

---

## 🔐 Segurança

### Assinatura de Commits com GPG
```bash
# Configurar GPG
git config --global user.signingkey {key-id}
git config --global commit.gpgsign true           # Assina todos os commits
git config --global tag.gpgsign true              # Assina todas as tags

# Verificar assinaturas
git log --show-signature                          # Mostra assinaturas
git verify-commit {hash}                          # Verifica commit
git verify-tag {tag}                              # Verifica tag
```

### Proteção de Dados Sensíveis
```bash
# Verificar se há segredos no histórico
git secrets --scan-history

# Usar git-crypt para criptografar arquivos
git-crypt init
git-crypt add-gpg-user {user-id}

# Configurar pre-commit hooks
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
# Verifica por palavras-chave sensíveis
if git diff --cached | grep -E "(password|api_key|secret|token)" ; then
    echo "ERRO: Possível dado sensível detectado!"
    exit 1
fi
EOF
chmod +x .git/hooks/pre-commit
```

---

## 📚 Recursos Adicionais

### Documentação Oficial
- 📖 [Git Documentation](https://git-scm.com/doc)
- 🐙 [GitHub Docs](https://docs.github.com/)
- 📘 [Pro Git Book](https://git-scm.com/book/en/v2)
- 🎓 [Git Tutorial - Atlassian](https://www.atlassian.com/git/tutorials)

---

## 🎯 Comandos Mais Usados - Quick Reference

```bash
# Top 10 comandos diários
git status                                        # Verifica estado
git add .                                         # Adiciona mudanças
git commit -m "msg"                               # Cria commit
git push                                          # Envia mudanças
git pull                                          # Recebe mudanças
git checkout -b feature                           # Nova branch
git merge feature                                 # Merge branch
git log --oneline                                 # Ver histórico
git stash                                         # Guardar mudanças
git diff                                          # Ver diferenças
```

---

## 🤝 Contribuindo

Encontrou um erro ou tem uma sugestão? Sinta-se à vontade para:
1. Abrir uma [issue](https://github.com/scaique/VersionamentoDeCodigoGit/issues)
2. Fazer um fork e enviar um Pull Request
3. Entrar em contato: [scaique.dev.br](https://scaique.dev.br)

---

## ⭐ Apoie este Projeto

Se este guia foi útil para você:
- ⭐ Dê uma estrela no [GitHub](https://github.com/scaique/VersionamentoDeCodigoGit)
- 🔗 Compartilhe com seus colegas
- 📢 Siga no GitHub para mais conteúdo

---

**Última atualização**: Dezembro 2025  
**Mantido por**: [Caique](https://github.com/scaique) | [Portfolio](https://scaique.dev.br)