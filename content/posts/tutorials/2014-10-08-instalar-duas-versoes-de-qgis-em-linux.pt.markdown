---

date: 2014-10-08 23:49:52+00:00
title: Instalar duas versões de QGIS em Linux
tags:
- linux
- master
- QGIS
---

[![QGIS24_QGISmaster](/images/2014/10/qgis24_qgismaster.png?w=584)
](/images/2014/10/qgis24_qgismaster.png)

Em altura de testes à versão em desenvolvimento do QGIS (versão master), dá jeito  ter também instalada a última versão estável do QGIS. Em windows isso não representa um problema, uma vez que se podem instalar várias versões do QGIS em paralelo (tanto via Osgeo4w como standalone). Em linux, o processo não é tão directo pelo facto da instalação se realizar por obtenção de diversos pacotes disponíveis nos repositórios, não sendo por isso possível instalar mais do que uma versão sem que se originem quebras de dependências. Assim, instalando a versão estável através dos repositórios, as alternativas para instalação da versão em desenvolvimento são:



	  * Compilar o QGIS master do código fonte;
	  * Instalar o QGIS master num docker;
	  * Instalar o QGIS master numa máquina virtual;

Neste artigo vou mostrar como compilar o código fonte em **Ubuntu 14.04**. Afinal não é tão difícil quanto parece. Meia dúzia de comandos e um pouco de paciência e vai-se lá. Usei como base as indicações do ficheiro [INSTALL.TXT](https://github.com/qgis/QGIS/blob/master/INSTALL) disponível no código fonte com umas pequenas alterações.

**Instalar todas as dependências necessárias**

Num terminal correr o seguinte comando para instalar todas as dependências e ferramentas necessárias à compilação do QGIS. (adicionei o ccmake e o git ao comando original)


    sudo apt-get install bison cmake doxygen flex git graphviz grass-dev libexpat1-dev libfcgi-dev libgdal-dev libgeos-dev libgsl0-dev libopenscenegraph-dev libosgearth-dev libpq-dev libproj-dev libqscintilla2-dev libqt4-dev libqt4-opengl-dev libqtwebkit-dev libqwt5-qt4-dev libspatialindex-dev libspatialite-dev libsqlite3-dev lighttpd pkg-config poppler-utils pyqt4-dev-tools python-all python-all-dev python-qt4 python-qt4-dev python-sip python-sip-dev spawn-fcgi txt2tags xauth xfonts-100dpi xfonts-75dpi xfonts-base xfonts-scalable xvfb cmake-curses-gui




# Configurar o ccache


Este passo permite optimizar a compilação e tornar a compilação mais rápida nas próximas vezes que se fizer:


    cd /usr/local/bin
    sudo ln -s /usr/bin/ccache gcc
    sudo ln -s /usr/bin/ccache g++




#  Obter o código fonte do Github


O código fonte pode ser colocado numa pasta à escolha de cada um. Seguindo a sugestão do ficheiro de instruções acabei por colocar tudo na minha pasta home/alexandre/dev/cpp.


    mkdir -p ${HOME}/dev/cpp
    cd ${HOME}/dev/cpp


Já dentro da pasta home/alexandre/dev/cpp, podemos obter o código do qgis executando o seguinte comando git:


    git clone git://github.com/qgis/QGIS.git


**Nota:** Se pretendesse fazer alterações ao código e experimentar se funcionava, então deveria fazer o clone do fork do qgis do meu próprio repositório, ou seja:


    git clone https://github.com/SrNetoChan/Quantum-GIS




# Preparar directorias de compilação e instalação


O código fonte tem de ser compilado e instalado em locais próprios para evitar conflitos com outras versões do QGIS. Por isso, há que criar uma pasta para efectuar a instalação:


    mkdir -p ${HOME}/apps


E outra onde será feita a compilação:


    cd QGIS
    mkdir build-master
    cd build-master





# Configuração


Já na pasta build-master damos início ao processo de compilação. O primeiro passo é a configuração, onde vamos dizer onde queremos instalar o QGIS master. Para isso executamos o seguinte comando (não esquecer os dois pontos):


    ccmake ..


Na configuração é necessário alterar o valor do CMAKE_INSTALL_PREFIX que define onde vai ser feita a instalação, no meu caso usei a pasta já criada 'home/alexandre/apps' . Para editar o valor há que mover o cursor até à linha em causa e carregar em [enter], depois de editar, volta-se a carregar em [enter]. Depois há que carregar em [c] para refazer a configuração e depois em 'g' para gerar a configuração.

[![Screenshot from 2014-10-08 23:33:39](/images/2014/10/screenshot-from-2014-10-08-233339.png?w=584)
](/images/2014/10/screenshot-from-2014-10-08-233339.png)


#  Compilação e instalação


Já com tudo configurado resta compilar o código e depois instalá-lo:


    make
    sudo make install


Nota: Estes dois passos podem demorar um bocadinho, principalmente na primeira vez que o código for compilado.

Depois de instalado podemos correr o QGIS master a partir da pasta de instalação:


    cd ${HOME}/apps/bin/
    export LD_LIBRARY_PATH=/home/alexandre/apps/lib
    export QGIS_PREFIX_PATH=/home/alexandre/apps
    ${HOME}/apps/bin/qgis


Para se tornar mais cómodo, podemos colocar os últimos 3 comandos num ficheiro .sh e gravá-lo num local acessível (desktop ou home) para executarmos o qgis sempre que necessário.

![Screenshot from 2014-10-09 00:36:52](/images/2014/10/screenshot-from-2014-10-09-003652.png?w=584)



# UPDATE: Actualizar a versão master


Como já foi referido num comentário, a versão em desenvolvimento está constantemente a ser alterada, por isso para testar se determinados bugs foram entretanto corrigidos há que a actualizar. Trata-se de um processo bastante simples. O primeiro passo é actualizar o código fonte:


    cd ${HOME}/dev/cpp/qgis
    git pull origin master


E depois é voltar a correr a compilação (que desta feita será mais rápida):


    cd build-master
    ccmake ..
    make
    sudo make install
