# git

### Configurações
```bash
# Configurações git do sistema
$ git config --system --edit

# Configurações git do usuário
$ git config --global --edit

# Configurações git do projeto
$ git config --edit
# or
$ git config --local --edit
```
#### Como criar alias
Execute o seguinte comando:
```console
admin:~$ git config --global --edit
```
Adicione o seguinte comando no arquivo .gitconfig aberto pelo editor:
```js
[alias]
  c = !git command
```
Agora, ao invés de usar `git command` use `git c`

### Criando commit e stash
```bash
# Adicionar arquivos na stage area
$ git add file_name # Adiciona arquivos específicos
$ git add . # Adiciona arquivos a partir do diretório atual em cascata para diretórios filhos.
$ git add --all # Adiciona todos os arquivos do projeto

# Criar um commit
$ git commit -m "message" # Cria um novo commit
$ git commit --amend --no-edit # Cria um commit mesclado com o anterior

# Colocar modificações no stash
$ git stash # Coloca todas as modificações no stash
$ git stash list # Listagem de stash salvos
$ git stash pop # Recupera modificações e limpa a lista
$ git stash apply # Recupera modificações
$ git stash clear # Limpa a lista
```

### Status dos arquivos
#### Untracked files
Arquivos desconhecidos pelo git.
```console
admin:~$ git status -s
?? index.js
```
#### Not staged
Arquivos reconhecidos mas que não foram adicionados ao git depois de modificados. Estão fora da stage area, portanto não irão entrar no próximo commit.
```console
admin:~$ git status -s
M index.js
```
#### Staged
Arquivos que irão entrar no próximo commit.
```console
admin:~$ git status -s
A index.js
```

### Auxiliary commands
```bash
# Exibir status dos arquivos modificados e branch atual
$ git status
# or
$ git status --s

# Exibir lista de commits
$ git log
# or
$ git log --oneline
```

#### Como adicionar git log personalizado no alias:
Adicione o seguinte comando ao alias:
```
l = !git log --pretty=format:'%C(green)%h %C(yellow)%d %C(white)%s - %C(cyan)%cn, %C(blue)%cr'
```
