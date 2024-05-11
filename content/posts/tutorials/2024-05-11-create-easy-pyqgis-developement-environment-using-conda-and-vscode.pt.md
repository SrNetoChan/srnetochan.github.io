---
title: "Criar um Ambiente de Desenvolvimento PyQGIS Usando Conda e VScode"
date: 2024-05-11T01:32:25Z
tags:
- pyqgis
- QGIS
- conda
- vscode
hero: /images/posts_hero/test_autocompletion.png
---

Como programador autodidata em PyQGIS, uma das minhas principais dificuldades sempre foi preparar um bom ambiente de desenvolvimento. Um ambiente que me permita executar scripts PyQGIS, que me ajude a programar mais rápido, que destaque e autocomplete PyQGIS, que me permita fazer debug dos meus plugins e scripts enquanto eles são executados, etc...

Tenho sido um utilizador (e até um... "cof cof"... *maintainer*) dos pacotes QGIS para conda fornecidos pela comunidade [conda-forge](https://conda-forge.org/). No Linux, isso permitiu-me instalar facilmente a versão LTR do QGIS (ou qualquer outra versão) ao lado da versão mais recente do QGIS fornecida pelos repositórios apt do qgis.org. Acabei por descobrir que este tipo de instalação também era bastante conveniente para desenvolvimento.

Quanto ao editor de text, tenho experimentado diversos editores/IDEs Python. Usei o Eric4, Geany, PyCharm (JetBrains), Atom (GitHub), mas agora uso o **VSCode** (Microsoft), ou antes, sua alternativa "Microsoft-less", o **VSCodium**. Devo dizer que gosto muito de usar o VSCode. Tem muitas funcionalidades base úteis e uma grande coleção de extensões que o tornam um editor de texto muito conveniente para trabalhar em muitas linguagens e formatos de programação diferentes (estou a usá-lo agora mesmo para escrever este post em Markdown). Também tem uma boa integração com ambientes Conda e git, o que acaba por ser uma grande ajuda.

Então, deixem-me descrever como configuro o meu Ambiente PyQGIS usando estas ferramentas.

**Nota:** Normalmente faço meu desenvolvimento em Linux, mas, como a maioria dos utilizadores estará em Windows, tentarei esclarecer algumas particularidades deste sistema operacional. Sinto muito pessoal do Mac OS, como sempre, vocês estão por vossa conta, pois não tenho como virtualizar o Mac OS (culpem a Apple por isso...), mas acho que é bastante semelhante ao Linux de qualquer forma.

### Instalar o conda

Existem vários instaladores que pode usar para instalar o conda no seu sistema, aqui estão alguns:

* [Anaconda (pela Anaconda inc)](https://www.anaconda.com/download#downloads)- Uma instalação completa do conda, já com muitos pacotes Python pré-instalados, muitos dos quais você provavelmente nunca irá usar
* [Miniconda (pela Anaconda inc)](https://docs.conda.io/en/latest/miniconda.html#latest-miniconda-installer-links) - Uma instalação mais leve do conda, contendo apenas as ferramentas conda e Python necessárias para instalar pacotes e gerir ambientes (escolha recomendada para iniciantes).
* [Miniforge (pela conda-forge)](https://github.com/conda-forge/miniforge#miniforge3)- Igual ao Miniconda, mas por conveniência, usa o canal conda-forge como padrão em vez do canal do anaconda.
* [Mambaforge](https://github.com/conda-forge/miniforge#mambaforge) - Similar ao Miniforge, mas contém ferramentas alternativas (`mamba` em vez de `conda`) para construir e instalar pacotes. Os comandos `mamba` são semelhantes, mas mais rápidos que os do `conda` (a minha escolha).

Escolha o que melhor se adequar às suas necessidades. Durante a instalação, pode usar todos as opções *default*.

### Criar um ambiente conda com QGIS

Vamos criar um novo ambiente conda, onde instalaremos o QGIS e quaisquer outros pacotes que possamos precisar. Este ambiente será isolado das suas restantes instalações, e por isso não afetará sua instalação principal do QGIS ou de Python.

Já descrevi a instalação do QGIS de uma forma mais detalhada noutro artigo [Usando o QGIS via conda](./2019-05-29-using-qgis-from-conda.markdown), mas tudo o que precisa fazer é executar o seguinte comando na consola/terminal (utilizadores Windows: precisam de usar o **Miniconda prompt**, não o *Command Prompt* normal) para criar um ambiente chamado *qgis_dev* com o QGIS instalado:

    conda create -n qgis_dev qgis -c conda-forge

Se precisar de uma versão específica do QGIS (normalmente uso a versão LTR para desenvolvimento), use algo assim:

    conda create -n qgis_dev qgis=3.34.6 -c conda-forge

Se quiser usar uma versão específica do Python, é semelhante:

    conda create -n qgis_dev qgis=3.34.6 python=3.10 -c conda-forge

Se estiver a usar mamba, substitua `conda` por `mamba` e não precisará especificar o canal conda-forge (além disso, aproveite a velocidade extra na instalação).

    mamba create -n qgis_dev qgis=3.34.6 python=3.10

Se estiver em Windows, como última etapa, certifique-se de fechar o *Miniconda prompt* antes de continuar.

### Instalar e configurar o VSCode ou Codium

Como disse antes, aqui há duas alternativas:

* [Visual Studio Code](https://code.visualstudio.com/download) - Produto da Microsoft que tem por omissão algumas opções de telemetria e rastreamento.
* [VS Codium](https://vscodium.com/) - uma distribuição binária livre e comunitária do editor VS Code da Microsoft, que tem as opções de telemetria desativadas. A instalação é um pouco mais complicada, mas nada de especial.

A forma de funcionamento é totalemente igual. Como tal... Os seus dados, a sua escolha.

Escolha o instalador correto de acordo com seu sistema operativo, arquitetura e permissões, e execute-o (para o Windows, há um instalador de utilizador que não precisa de privilégios de administração).

Use as opções *default* durante a instalação. Em Windows, certifique-se de selecionar a opção `Add to PATH (requires shell restart)`. Isso irá permitir abrir o VSCode facilmente a partir da linha de comando. Em Linux, isso já vem por defeito.

Agora, vamos abrir o VSCode e instalar a extensão Python.

Para instalar uma extensão no VSCode, clique no separador das extensões no painel esquerdo. Em seguida, pesquise pelo nome da extensão. No nosso caso, procure por `python` e depois selecione a extensão **Python** de **ms-python** e clique em instalar. Isso adicionará o IntelliSense (Pylance), Linting, Debugging
(multi-threaded, remote), Jupyter Notebooks, code formatting, refactoring,
unit tests, e outros.

![Buscar Extensão Python](/images/2024/05/install_python_extension.png)

Pode, é claro, instalar outras extensões, mas por enquanto, esta é suficiente.

O último passo, **FECHAR O VSCode**.

### Como usar o ambiente PyQGIS

As passos acima só precisam ser feitos uma vez. Os seguintes passos são o que precisa de fazer sempre que quiser usar o ambiente PyQGIS preparado.

Nota: Se instalou o VSCode com o *Miniconda prompt* aberto, feche-o (é a parte que requer reinicialização do shell)

1. Abra o **Terminal** (Linux e Mac) ou o **Miniconda prompt** (Windows).
2. Ative o ambiente qgis_dev

       conda activate qgis_dev

3. Abra o VS Code escrevendo `code` no terminal e pressionando ENTER.

4. No VSCode, vá a **File > Open Folder** e selecione a sua pasta de trabalho (aquela que irá usar para o desenvolvimento). Alternativamente, pode navegar até a pasta desejada usando a linha de comando e abrir o VSCode escrevendo `code .`

Está tudo pronto. Agora pode começar a escrever scripts ou plugins PyQGIS e o VS Code conhecerá os pacotes e módulos do QGIS, destacará o código e fará autocomplete.

Para testar se tudo está a funcionar conforme o esperado, pode criar um arquivo Python vazio (**File > New File > Python File**), por exemplo, `test_pyqgis.py` e começar a escrever o seguinte:

    from qgis.core import Qgs

Depois de escrever `Qgs` deverá ver a lista de módulos do **qgis.core** numa combobox (pode demorar um pouco na primeira vez). Além disso, no canto direito da tela, deve ver algo como `3.11.4 64bit`. Se passar o rato por cima, deverá ver a localização do ambiente conda *qgis_dev*. Isso significa que o VSCode está a usar o ambiente python *qgis_dev* e não qualquer outro.

![Teste de Autocompletar do QGIS](/images/2024/05/test_autocompletion.png)