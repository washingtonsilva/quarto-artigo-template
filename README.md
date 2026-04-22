# quarto-artigo-template

## Pré-requisitos

Para utilizar este template, os seguintes softwares devem estar instalados e funcionais:

| Software | Finalidade | Status |
|---|---|---|
| [R](https://cran.r-project.org/) | Linguagem de programação estatística | Necessário |
| [RStudio](https://posit.co/download/rstudio-desktop/) | Ambiente de desenvolvimento (IDE) | Necessário |
| [Quarto](https://quarto.org/docs/get-started/) | Sistema de publicação para geração do PDF | Necessário |
| [Git para Windows](https://git-scm.com/download/win) | Controle de versão e integração com o GitHub | Necessário |
| [TinyTeX](https://yihui.org/tinytex/) | Distribuição LaTeX para compilação do PDF | **Instalar** |

Antes de começar, recomenda-se fortemente atualizar o **RStudio** e o **Quarto** para as versões mais recentes, a fim de evitar incompatibilidades.

### Instalando o TinyTeX

O TinyTeX é a única dependência que provavelmente ainda não está instalada. Trata-se de uma distribuição LaTeX leve, desenvolvida especificamente para uso com R e Quarto, e que pode ser instalada diretamente do console do RStudio em dois passos.

**Passo 1 —** Instale o pacote `tinytex` do R:

```r
install.packages("tinytex")
```

**Passo 2 —** Execute a instalação da distribuição LaTeX:

```r
tinytex::install_tinytex()
```

A instalação pode levar alguns minutos. Ao final, **reinicie o RStudio** antes de tentar renderizar o documento.

> **Observação:** o arquivo `01_capm.qmd` inclui a opção `latex-auto-install: true` no seu cabeçalho YAML. Isso faz com que o Quarto instale automaticamente eventuais pacotes LaTeX adicionais na primeira renderização, sem necessidade de intervenção manual.

### Pacotes R necessários

Os seguintes pacotes R são utilizados no documento e devem ser instalados antes da primeira renderização:

```r
install.packages(c("here", "tidyverse", "gtsummary", "modelsummary", "kableExtra", "moments"))
```

## Como Criar seu Repositório a partir deste Template

Este projeto foi publicado no **GitHub** como um **template**. Para criar sua cópia e começar a trabalhar:

1. Acesse esta página do repositório no **GitHub**.
2. Clique em `Use this template` e em seguida em `Create a new repository`.
3. Dê um nome ao seu repositório. Recomenda-se o padrão `artigo_nome_sobrenome` (por exemplo: `artigo_joao_silva`), mas a escolha é livre, desde que sejam seguidas boas práticas de nomeação: use *snake_case*, sem acentos, espaços ou caracteres especiais.
4. Mantenha o repositório como **público**.
5. Clique em `Create repository` e copie a URL do repositório criado.
6. Abra o **RStudio**.
7. Clique em `Project > New Project > Version Control > Git`.
8. Cole a URL do repositório no campo `Repository URL`.
9. No campo `Project directory name`, verifique se o nome do repositório foi preenchido automaticamente. Se não, escreva-o manualmente.
10. Escolha a pasta em que o projeto será salvo no seu computador.
11. Clique em `Create Project`. O **RStudio** clonará o repositório e abrirá o projeto localmente.
12. Renderize o arquivo `01_capm.qmd` para verificar se tudo está funcionando corretamente.

A renderização criará o arquivo `01_capm.pdf` na pasta do projeto. Esse **PDF** não é versionado pelo **Git**, pois é gerado automaticamente a partir do arquivo-fonte.

> **Observações:**
> - ao clonar pelo **RStudio**, o próprio **RStudio** criará automaticamente um arquivo de projeto `.Rproj` com o nome do repositório local;
> - esse arquivo `.Rproj` é apenas local e não faz parte do conteúdo versionado do template.

## Estrutura do Repositório

Após clonar o repositório, você encontrará a seguinte estrutura de arquivos e pastas:

```
quarto-artigo-template/
│
├── 01_capm.qmd                                    # Documento principal do artigo
├── referencias.bib                                # Referências bibliográficas em formato BibTeX
├── associacao-brasileira-de-normas-tecnicas-ipea.csl  # Estilo de citação ABNT (via IPEA)
├── .gitignore                                     # Arquivos e pastas ignorados pelo Git
│
└── data/
    └── clean/
        └── dados_capm_clean.rds                   # Dados processados utilizados no documento
```

### Descrição dos arquivos

**`01_capm.qmd`** é o arquivo central do template. Escrito em formato Quarto Markdown (`.qmd`), ele reúne em um único documento o texto do artigo, o código R e as instruções de formatação do PDF. É o único arquivo que você editará regularmente.

**`referencias.bib`** contém as referências bibliográficas no formato BibTeX. Cada entrada corresponde a uma obra citada no texto. Para adicionar novas referências, basta incluir novos registros neste arquivo — o Quarto cuidará automaticamente da formatação e da lista de referências ao final do documento.

**`associacao-brasileira-de-normas-tecnicas-ipea.csl`** define o estilo de citação utilizado, seguindo as normas da ABNT. O arquivo está no formato CSL (*Citation Style Language*) e não precisa ser modificado.

**`.gitignore`** lista os arquivos e pastas que o Git deve ignorar, como arquivos temporários do sistema operacional, arquivos auxiliares do LaTeX e o PDF gerado. Não é necessário modificá-lo.

**`data/clean/dados_capm_clean.rds`** contém os dados já processados que alimentam as análises do documento — retornos excedentes da Ford e do índice S&P 500. O formato `.rds` é nativo do R. Ao adaptar o template para seu próprio artigo, substitua este arquivo pelos seus dados.

## O Cabeçalho YAML do Documento

Todo documento Quarto começa com um cabeçalho YAML, o bloco delimitado por `---` no início do arquivo. Ele concentra as configurações do documento: metadados, formato de saída, comportamento do código e referências bibliográficas. Abaixo, cada opção do cabeçalho de `01_capm.qmd` é explicada.

### Metadados do documento

```yaml
title: "Estimação do Modelo CAPM"
subtitle: "Working Paper"
author: Seu Nome
lang: pt-BR
```

`title` e `subtitle` definem o título e o subtítulo que aparecerão na capa do PDF. `author` deve ser substituído pelo seu nome. `lang: pt` informa ao Quarto que o documento está em português brasileiro, o que afeta a hifenização automática do LaTeX e os rótulos gerados automaticamente.

### Formato de saída

```yaml
format:
    pdf:
        documentclass: article
        papersize: a4paper
        fontsize: 12pt
        linestretch: 1.0
        number-sections: true
        indent: true
        tbl-pos: 'H'
        fig-pos: 'H'
        colorlinks: TRUE
        linkcolor: blue
        link-citations: true
        latex-auto-install: true
        include-in-header:
            - text: |
                    \usepackage{indentfirst}
```

Todas as opções abaixo de `pdf:` controlam a aparência do documento gerado.

- `documentclass: article` define a classe do documento LaTeX. `article` é a classe padrão para artigos científicos.
- `papersize: a4paper` define o tamanho do papel como A4.
- `fontsize: 12pt` define o tamanho da fonte principal.
- `linestretch: 1.0` define o espaçamento entre linhas. Altere para `1.5` ou `2.0` para espaçamento maior, se necessário.
- `number-sections: true` numera automaticamente as seções do documento.
- `indent: true` ativa o recuo no início de cada parágrafo.
- `tbl-pos: 'H'` e `fig-pos: 'H'` instruem o LaTeX a posicionar tabelas e figuras exatamente onde aparecem no texto, evitando deslocamentos automáticos.
- `colorlinks: TRUE` e `linkcolor: blue` tornam os hiperlinks clicáveis e os colorem em azul no PDF.
- `link-citations: true` transforma cada citação no texto em um hiperlink que leva à entrada correspondente na lista de referências.
- `latex-auto-install: true` permite que o Quarto instale automaticamente pacotes LaTeX ausentes durante a renderização.
- `include-in-header` com `\usepackage{indentfirst}` carrega o pacote LaTeX que garante recuo também no primeiro parágrafo de cada seção.

### Referências bibliográficas

```yaml
bibliography: referencias.bib
csl: associacao-brasileira-de-normas-tecnicas-ipea.csl
```

`bibliography` aponta para o arquivo BibTeX com as referências. `csl` define o estilo de citação, neste caso, ABNT. Ambos os arquivos já estão incluídos no repositório e só precisam ser alterados se você quiser adotar outro estilo de citação.

### Referências cruzadas

```yaml
crossref:
    fig-prefix: 'Fig.'
    tbl-prefix: 'Tab.'
```

Essa configuração define os prefixos usados nas referências cruzadas automáticas a figuras e tabelas. Com isso, ao usar `@fig-dispersao`, o Quarto exibirá algo como "Fig. 1" no PDF.

### Execução do código R

```yaml
execute:
    echo: false
    message: false
    warning: false
    enabled: true
```

Essas opções controlam o comportamento global dos blocos de código R no documento.

- `echo: false` faz com que o código não apareça no PDF, apenas seus resultados.
- `message: false` suprime mensagens geradas pelos pacotes R.
- `warning: false` suprime avisos gerados pelo R.
- `enabled: true` garante que o código será executado durante a renderização.

Essas opções podem ser sobrescritas individualmente em cada bloco de código com diretivas como `#| echo: true`.

### Opções finais

```yaml
editor: source
keep-tex: true
```

`editor: source` instrui o RStudio a abrir o arquivo no modo de edição de código-fonte. `keep-tex: true` preserva o arquivo `.tex` intermediário gerado durante a compilação, o que ajuda a depurar problemas de formatação no LaTeX.
