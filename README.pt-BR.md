# git-guide
> Esse é um guia de comandos Git que contém exemplos e explicações dos seus diferentes casos de uso, além de links para as documentações oficiais.

*Ler em outros idiomas: [English](/README.md)*

---

### [Configurações](https://git-scm.com/docs/git-config/pt_BR)
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
#### Como criar [alias](https://git-scm.com/docs/git-config#Documentation/git-config.txt-alias)
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

### Criando [commit](https://git-scm.com/docs/git-commit/pt_BR) e [stash](https://git-scm.com/docs/git-stash/pt_BR)
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

### [Status](https://git-scm.com/docs/git-status/pt_BR) dos arquivos
#### Untracked files
Arquivos desconhecidos pelo git.
```console
admin:~$ git status -s
?? index.js
```
#### Not staged (Unstaged area)
Arquivos reconhecidos mas que não foram adicionados ao git depois de modificados. Estão fora da stage area, portanto não irão entrar no próximo commit.
```console
admin:~$ git status -s
M index.js
```
#### Staged (Staging area / Index)
Arquivos que irão entrar no próximo commit.
```console
admin:~$ git status -s
A index.js
```

### Comandos auxiliares
[status](https://git-scm.com/docs/git-status/pt_BR), [show](https://git-scm.com/docs/git-show/pt_BR) e [log](https://git-scm.com/docs/git-log/pt_BR)
```bash
# Exibir status dos arquivos modificados e branch atual
$ git status
# ou
$ git status --s

# Exibir detalhes de algum commit especifico
$ git show [commit_ref]
# ou
$ git show [commit_ref] --oneline

# Exibir lista de commits
$ git log
# ou
$ git log --oneline
```

#### Como adicionar [git log personalizado](https://git-scm.com/docs/git-log/pt_BR#_formatos_bonitos) no alias:
Adicione o seguinte comando ao alias:
```
l = !git log --pretty=format:'%C(green)%h %C(yellow)%d %C(white)%s - %C(cyan)%cn, %C(blue)%cr'
```
Nova saída do *git log*:
<p><img src="/samples/log.png"></p>

### [Tags](https://git-scm.com/docs/git-tag/pt_BR)
```bash
# Criar uma nova tag
$ git tag v1.0 hash_commit # Cria uma Lightweight tag
$ git tag v1.0 -m "Release v1.0" hash_commit # Cria uma Annotated tag (Ideal para enviar ao Github)

# Exbir tags
$ git tag # Exibe todas as tags
$ git tag v1.0 # Exibe tag específica

# Deletar tag
$ git tag --delete v1.0 # Deleta do git local
$ git push --delete origin v1.0 # Deleta do git remoto
```
#### Enviar Annotated tags para o GitHub
Abra as configurações git de usuário `--global`, e adicione o seguinte código:
```js
  [push]
    followTags = true
```

### [Checkout](https://git-scm.com/docs/git-checkout/pt_BR)
```bash
$ git checkout . # Desfaz as alterações dos arquivos que estão na Unstaged area e estão tracked.
$ git checkout [[commit_ref] or [tag_ref]] # Cria uma branch virtual com o ponto escolhido para análise do códico naquele ponto.
$ git checkout -b nome_branch # Cria uma branch real
$ git checkout nome_branch # Muda para a branch

```
### [Merge](https://git-scm.com/docs/git-merge/pt_BR)
```bash
$ git merge branch_name . # Merge a branch atual com a branch_name.

```

### [Git reset](https://git-scm.com/docs/git-reset/pt_BR)

#### Estrutura padrão
```bash
$ git reset [hash or HEAD~n] --flag
```
*HEAD* - Último commit
####
*n* - Quantidade de commits a baixo do HEAD
####
*hash* - Hash do commit (O default é o ultimo commit, ou seja, o HEAD)
####
*--flag* - pode ser --soft, --mixed (default), --hard

#### Exemplos
  ```bash
  # Manipulando commits
  $ git reset HEAD~1 --soft # Volta para o commit anterior colocando os arquivos na Staging area.
  $ git reset HEAD~2 --mixed # Volta 2 commits colocando os arquivos de volta na Unstaged area.
  $ git reset HEAD~1 --hard # Volta para o commit anterior e desfaz a modificação dos arquivos do Unstaged area.
  
  # Manipulando commit atual (HEAD)
  # O default para este comando é o HEAD, portanto, se não for passado nada na referência do commit, ele irá tratar do último commit.
  $ git reset # Tag --mixed omitida. Volta os arquivos da Staging Area para a Unstaged area.
  $ git reset --hard # Desfaz a modificação dos arquivos que estão na Unstaged area ou Staging area.
  ```

### [Revert](https://git-scm.com/docs/git-revert/pt_BR)
#### Estrutura
```bash
$ git revert [hash ou HEAD~1] --flag
```
#### Examples
```bash
$ git revert HEAD~1 # Cria um novo commit com as modificações contrarias ao do commit atual.
$ git revert HAAD~1 --no-edit # Cria um novo commit sem abrir um arquivo no editor.
$ git revert HEAD~1 --no-commit # Faz as alterações contrárias nos arquivos e os adiciona a Staging area.
```

### [Clean](https://git-scm.com/docs/git-clean/pt_BR)
#### Estrutura
```bash
$ git clean --flag
```
#### Exemplos
```bash
$ git clean -n # Mostra os untracked files.
$ git clean -n -d # Mostra todos os untracked files de forma recursiva.
$ git clean -f # Deleta os untracked files.
$ git clean -f -d # Deleta todos os untracked files de forma recursiva.
```

### [Rm](https://git-scm.com/docs/git-rm/pt_BR)
#### Estrutura
```bash
$ git rm file.ex --flag
```
#### Exemplos
```bash
$ git rm index.js # Remove o tracked file.
$ git rm folder -r # Deleta os tracked files de forma recursiva.
```
#### Como ignorar arquivos que já estão tracked.
Execute o seguinte comando:
```bash
$ git rm index.js --cached'
```

### [Rebase](https://git-scm.com/docs/git-rebase/pt_BR)
Execute o seguinte comando para abrir no editor:
```bash
$ git rebase -i [commit_ref]'
```

#### Comandos
```bash
# p, pick <commit> = use o commit.
# r, reword <commit> = use o commit, mas edite a messagem dele.
# e, edit <commit> = use o commit, mas você pode parar para juntar com outros também.
# s, squash <commit> = use o commit, mas você pode fundi-lo com o commit anterior.
# f, fixup <commit> = use como "squash", mas descarte a mensagem de log deste commit.
# x, exec <command> = execute o comando usando shell.
# b, break = pause aqui (continue o rebase depois com 'git rebase --continue')
# d, drop <commit> = remove o commit.
# l, label <label> = rotula o HEAD atual com um nome.
# t, reset <label> = redefinir HEAD para um rótulo especifico.
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       cria um merge commit usando a mensagem original dos merge commits 
#         (ou o oneline, se o merge commit original foi especificado). 
#         Use -c <commit> para reformular a menssagem do commit.
```

Feche o editor ou use a flag ```---abort``` para sair do modo *rebasing*.
```bash
$ git rebase --abort'
```

