# quarto-artigo-template

Este repositório é um template para a criação de artigos científicos com o [Quarto](https://quarto.org/), desenvolvido no âmbito da disciplina **Introdução à Ciência de Dados** do Mestrado Profissional em Administração do IFMG — Campus Formiga.

O objetivo é duplo: por um lado, apresentar uma estrutura funcional de documento reprodutível que integra texto, código R e saída formatada em PDF via LaTeX; por outro, servir de pretexto para a prática de um fluxo de trabalho com **Git** e **GitHub** — desde a criação do repositório a partir de um template até o versionamento das alterações realizadas.

O documento de exemplo estima o Modelo de Precificação de Ativos de Capital (CAPM) como um modelo de regressão linear simples, contextualizando o template na área de concentração em **Finanças** do programa.

## Pré-requisitos

Para utilizar este template, os seguintes softwares devem estar instalados e funcionais:

| Software | Finalidade | Status |
| --- | --- | --- |
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
install.packages(c("here", "tidyverse", "modelsummary", "kableExtra", "moments"))
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
>
> - ao clonar pelo **RStudio**, o próprio **RStudio** criará automaticamente um arquivo de projeto `.Rproj` com o nome do repositório local;
> - esse arquivo `.Rproj` é apenas local e não faz parte do conteúdo versionado do template.

## Estrutura do Repositório

Após clonar o repositório, você encontrará a seguinte estrutura de arquivos e pastas:

```text
quarto-artigo-template/
│
├── 01_capm.qmd                                    # Documento principal do artigo
├── referencias.bib                                # Referências bibliográficas em formato BibTeX
├── associacao-brasileira-de-normas-tecnicas-ipea.csl  # Estilo de citação ABNT (via IPEA)
├── .gitignore                                     # Arquivos e pastas ignorados pelo Git
├── README.md                                      # Documentação do repositório
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

### Separação entre projeto analítico e projeto de escrita

Em projetos de pesquisa mais extensos — como uma dissertação de mestrado ou um artigo com pipeline de dados complexo —, recomenda-se fortemente manter **dois repositórios separados**:

**Projeto analítico** — responsável pela aquisição e preparação dos dados, pela estimação dos modelos e pela geração dos resultados finais. Este projeto tende a ser iterativo: modelos são revisados, decisões metodológicas são ajustadas, dados são reprocessados. Quando a análise estiver concluída e os resultados validados, o projeto é finalizado.

**Projeto de escrita** — responsável pela redação do documento final (dissertação, artigo ou relatório). Recebe os resultados do projeto analítico na forma de arquivos prontos para uso: objetos R salvos em `.rds`, figuras em `.png` ou `.pdf`, e tabelas em `.csv`. É sobre este projeto que o Quarto opera para gerar o PDF final.

Essa separação oferece três vantagens concretas: o histórico do Git de cada repositório permanece legível e focado; dados sensíveis ou proprietários ficam restritos ao projeto analítico, que pode ser mantido privado; e o projeto de escrita permanece limpo, sem código de preparação de dados que não é relevante para a comunicação dos resultados.

O ponto crítico dessa abordagem é a **rastreabilidade da transferência de resultados**. Ao copiar arquivos do projeto analítico para a pasta `data/` do projeto de escrita, documente no `README` do projeto de escrita qual versão (commit) do projeto analítico gerou aqueles resultados. Sem esse registro, torna-se difícil, meses depois, reproduzir ou auditar os resultados apresentados no documento.

## O Cabeçalho YAML do Documento

Todo documento Quarto começa com um cabeçalho YAML, o bloco delimitado por `---` no início do arquivo. Ele concentra as configurações do documento: metadados, formato de saída, comportamento do código e referências bibliográficas. Abaixo, cada opção do cabeçalho de `01_capm.qmd` é explicada.

### Metadados do documento

```yaml
title: "Estimação do Modelo CAPM"
subtitle: "Working Paper"
author: Seu Nome
lang: pt
```

`title` e `subtitle` definem o título e o subtítulo que aparecerão na capa do PDF. `author` deve ser substituído pelo seu nome. `lang: pt` informa ao Quarto que o documento está em português, o que afeta a hifenização automática do LaTeX e os rótulos gerados automaticamente.

### Resumo e palavras-chave

```yaml
abstract: |
  Texto do resumo.
  \linebreak \textbf{Palavras-chave:} palavra1, palavra2.
```

O campo `abstract` recebe o resumo do artigo. O símbolo `|` indica ao YAML que o conteúdo é um bloco de texto com múltiplas linhas, preservando as quebras de linha tal como escritas. Substitua o texto pelo resumo do seu artigo.

As palavras-chave são incluídas ao final do próprio resumo, usando dois comandos LaTeX diretamente no texto: `\linebreak` força uma quebra de linha antes das palavras-chave, e `\textbf{}` as formata em negrito. Essa abordagem é necessária porque a classe `article` do LaTeX não possui um campo nativo para palavras-chave — elas são incorporadas ao resumo por convenção.

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

### Tipos de comentários em um arquivo `.qmd`

Um arquivo `.qmd` pode conter três tipos de comentários, cada um com escopo e sintaxe diferentes. Compreender essa distinção é importante para usar o template corretamente.

**Comentários em prosa — `<!-- comentário -->`**

Utilizados no corpo do texto, fora dos chunks de código. São processados e descartados pelo Pandoc antes de qualquer compilação, de modo que **não aparecem em nenhum formato de saída** — nem no PDF, nem em HTML, nem em DOCX. Esse é o tipo de comentário usado nas seções de Introdução, Resultados e Conclusões do template para deixar orientações ao autor sem que elas apareçam no documento final.

```markdown
<!-- Este texto não aparecerá no PDF. -->
```

**Comentários em código R — `#`**

Utilizados dentro dos chunks de código R. São ignorados pelo interpretador R durante a execução e, como o YAML define `echo: false`, também não aparecem no PDF.

```r
# este comentário não aparece no PDF
media <- mean(x)  # comentário inline também não aparece
```

**Comentários LaTeX — `%`**

Utilizados exclusivamente dentro de blocos de código LaTeX bruto (delimitados por ```` ```{=latex} ````). São ignorados pelo compilador LaTeX e não aparecem no PDF.

```latex
% este comentário só funciona em blocos LaTeX brutos
\textbf{texto em negrito}
```

Em resumo: para deixar anotações e instruções invisíveis no corpo do texto de um `.qmd`, use sempre `<!-- -->`.

## Exercícios

### Exercício 1 — Inspecionando Alterações com `git diff`

Até agora você praticou os comandos essenciais para sincronizar seu repositório local com o GitHub: `git add`, `git commit` e `git push`. Este exercício introduz o comando `git diff`, que permite inspecionar exatamente o que foi alterado em um arquivo antes de registrar as mudanças com um commit.

#### O que é `git diff`?

O comando `git diff` compara o estado atual dos arquivos no seu diretório de trabalho com o último commit registrado, exibindo linha a linha o que foi removido e o que foi adicionado. Na saída do comando:

- linhas precedidas por `-` (em vermelho no terminal) indicam o conteúdo que existia antes;
- linhas precedidas por `+` (em verde no terminal) indicam o conteúdo novo que substituiu o anterior;
- linhas sem prefixo são o contexto ao redor da alteração e não foram modificadas.

Executar `git diff` antes de `git add` é uma boa prática: permite revisar as mudanças e confirmar que apenas o que se deseja está sendo versionado.

#### Tarefa do Exercício 1

Abra o arquivo `01_capm.qmd` no RStudio e faça as duas alterações abaixo no cabeçalho YAML:

**1.** Substitua `Seu Nome` pelo seu nome completo:

```yaml
# antes
author: Seu Nome

# depois
author: João Silva
```

**2.** Altere o espaçamento entre linhas de `1.0` para `1.5`:

```yaml
# antes
linestretch: 1.0

# depois
linestretch: 1.5
```

Salve o arquivo sem fechar o RStudio.

#### Executando `git diff`

No terminal do RStudio (aba **Terminal**), execute:

```bash
git diff 01_capm.qmd
```

#### Interpretando a saída

A saída esperada será semelhante a:

```diff
diff --git a/01_capm.qmd b/01_capm.qmd
--- a/01_capm.qmd
+++ b/01_capm.qmd
@@ -1,14 +1,14 @@
 ---
 title: "Estimação do Modelo CAPM"
 subtitle: "Working Paper"
-author: Seu Nome
+author: João Silva
 lang: pt
 format:
   pdf:
     documentclass: article
     papersize: a4paper
     fontsize: 12pt
-    linestretch: 1.0
+    linestretch: 1.5
     number-sections: true
     indent: true
```

Lendo a saída de cima para baixo:

- `--- a/01_capm.qmd` e `+++ b/01_capm.qmd` identificam o arquivo comparado: `a/` é a versão do último commit, `b/` é a versão atual no disco.
- `@@ -1,14 +1,14 @@` indica o intervalo de linhas exibido: antes e depois da alteração, o trecho vai da linha 1 até a linha 14.
- As duas linhas com `-` mostram exatamente o que existia no commit anterior.
- As duas linhas com `+` mostram o que passou a existir após suas edições.
- As demais linhas, sem prefixo, são o contexto — estão ali apenas para situar as mudanças e não foram tocadas.

#### Boas práticas para mensagens de commit em escrita acadêmica

A mensagem de commit é o registro permanente do que foi feito e por quê. Em projetos de desenvolvimento de software, é comum o uso de prefixos como `feat:` ou `fix:` — uma convenção que não se aplica naturalmente ao contexto acadêmico. Para artigos e dissertações, o que importa é que o histórico de commits narre com clareza a evolução do documento.

Algumas orientações práticas:

- **Comece com um verbo no infinitivo** que descreva a ação realizada: *adiciona*, *revisa*, *corrige*, *completa*, *reestrutura*, *atualiza*.
- **Identifique o que foi alterado** — a seção, o elemento ou o arquivo afetado. O objetivo é que qualquer pessoa (ou você mesmo, semanas depois) entenda o que aconteceu apenas lendo o log.
- **Seja específico, mas conciso.** Uma linha bem escrita é suficiente na maioria dos casos.
- **Evite mensagens vagas** como "atualiza arquivo", "correções" ou "mudanças diversas" — elas não acrescentam nenhuma informação ao histórico.

Exemplos de boas mensagens para o contexto acadêmico:

```text
adiciona rascunho da seção de revisão da literatura
revisa metodologia: inclui equação do modelo CAPM
corrige referência de Sharpe (1964) no arquivo .bib
atualiza tabela de estatísticas descritivas
completa seção de conclusões
```

#### Registrando as alterações

Após verificar que a saída do `git diff` corresponde ao esperado, registre as alterações seguindo as boas práticas acima:

```bash
git add 01_capm.qmd
git commit -m "personaliza autor e espaçamento do documento"
git push origin main
```

### Exercício 2 — Clonando um Repositório Existente

No exercício anterior, você criou um repositório **a partir de um template** — o que gerou um novo repositório em sua conta no GitHub. Agora você vai praticar uma operação diferente: **clonar** um repositório existente, criando apenas uma cópia local sem gerar um novo repositório no GitHub.

Essa distinção é importante: usar um template é o fluxo adequado quando você inicia um projeto próprio; clonar é o fluxo adequado quando você deseja obter uma cópia local de um repositório já existente para explorá-lo ou contribuir com ele.

#### Tarefa do Exercício 2

Clone o template de projeto de pesquisa para o exame de qualificação do mestrado, disponível em:

[https://github.com/washingtonsilva/quarto_exame_qualificacao](https://github.com/washingtonsilva/quarto_exame_qualificacao)

#### Passo a passo no RStudio

1. Abra o **RStudio**.
2. Clique em `Project > New Project > Version Control > Git`.
3. No campo `Repository URL`, cole a URL do repositório:

   ```
   https://github.com/washingtonsilva/quarto_exame_qualificacao.git
   ```

4. No campo `Project directory name`, verifique se o nome `quarto_exame_qualificacao` foi preenchido automaticamente.
5. Escolha a pasta em que o projeto será salvo no seu computador.
6. Clique em `Create Project`. O **RStudio** clonará o repositório e abrirá o projeto localmente.

#### O que fazer após clonar

Renderize o documento principal do repositório clonado para verificar se o ambiente está configurado corretamente. Se a renderização concluir sem erros e gerar o PDF, seu ambiente está pronto para ser utilizado quando você iniciar seu projeto de pesquisa.

Em seguida, explore a estrutura de arquivos e pastas do repositório clonado e compare-a com a estrutura deste template. Observe as semelhanças e diferenças na organização dos arquivos e no cabeçalho YAML do documento principal.

> **Observação:** como este é um clone de um repositório que não pertence à sua conta do GitHub, você não terá permissão para fazer push de alterações. Para criar sua própria cópia editável no momento certo, você utilizará o fluxo com `Use this template`, da mesma forma que fez ao criar seu repositório a partir deste template.
