# Publicar no GitHub

Este projeto ja esta preparado como repositorio Git local.

## Opcao 1: pelo site do GitHub

1. Crie um repositorio chamado `FocusCorreio`.
2. Nao marque para criar README, `.gitignore` ou LICENSE, porque o projeto ja tem esses arquivos.
3. Copie a URL do repositorio.
4. No PowerShell, dentro da pasta do projeto, rode:

```powershell
git remote add origin https://github.com/SEU_USUARIO/FocusCorreio.git
git push -u origin main
```

## Opcao 2: pelo GitHub CLI

Se o `gh` estiver instalado e logado:

```powershell
gh repo create FocusCorreio --public --source . --remote origin --push
```

Para criar privado:

```powershell
gh repo create FocusCorreio --private --source . --remote origin --push
```

## Estrutura do repositorio

```text
FocusCorreio/
  src/
  docs/
  .github/
  README.md
  CHANGELOG.md
  LICENSE
  build.ps1
```

## Antes de publicar uma release

1. Rode o build:

```powershell
.\build.ps1
```

2. Envie o arquivo gerado:

```text
build/FocusCorreio.jar
```
