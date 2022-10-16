---

date: 2014-03-25 08:41:42+00:00
title: Multipart Split
menu:
  sidebar:
    name: Multipart Split
    identifier: multipart-split
    parent: plugins
    weight: 20

---

O módulo (plugin) para QGIS Multipart Spliticon permite, durante a edição, separar elementos multipartes seleccionados transformando-os em elementos simples. Ao contrário da funcionalidade “Multipartes para partes simples” do menu Vector > Ferramentas de Geometria, o plugin permite separar apenas os elementos seleccionados, e não necessita de criar novos ficheiros.

### Instalação

O plugin está disponível no repositório oficial do QGIS, portanto a sua instalação pode ser feita através do instalador de módulos python (Módulos > Gerir e instalar módulos…).

### Utilização

Estando seleccionada uma camada vectorial em modo de edição (Camada > Alternar edição), seleccione todos os elementos que pretende separar e carregue no ícone do plugin que está disponível na barra de ferramentas “Vectorização Avançada” (Ver > Barras de Ferramentas > Vectorização Avançada) ou em Editar > Separar Partes do(s) elementos. No final do processo, uma mensagem no topo do mapa informa o resultado do processo. (Note que o ícone apenas fica activo se seleccionar uma camada em modo de edição, com pelo menos um elemento seleccionado)


Página: http://plugins.qgis.org/plugins/splitmultipart/

Repositório: https://github.com/SrNetoChan/MultipartSplit