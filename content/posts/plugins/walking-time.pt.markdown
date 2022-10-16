---

date: 2014-03-25 08:41:42+00:00
title: Walking time
menu:
  sidebar:
    name: Walking time
    identifier: walking-time
    parent: plugins
    weight: 20

---


O **Walking time** é um plugin python para QGIS que usa a Tobbler’s hiking function para estimar o tempo de percurso ao longo de uma linha consoante o declive.

Os dados de input necessários são uma camada vectorial de linhas e uma camada raster com valores de elevação (1). É possível ajustar a velocidade base (em terreno plano) de acordo com o tipo de caminhada ou caminhante. Por defeito, o valor usado é de 5 kmh (2). O plugin actualiza ou cria campos com o tempo estimado em minutos, no sentido directo e no sentido inverso (3). É possível correr o plugin para todos os elementos da camada vectorial, ou apenas nos percursos seleccionados (4).

O plugin pode também ser usado para preparar uma rede (grafo) para realizar análise de redes onde se queira usar como custo o tempo de percurso.

Captura de tela 2014-03-24 12.12.17-01

Repositório QGIS: http://plugins.qgis.org/plugins/walkingtime/

Código: https://github.com/SrNetoChan/WalkingTime

Reportar bugs: https://github.com/SrNetoChan/WalkingTime/issues

### Instalação

O plugin está disponível no repositório oficial de plugins do qgis. Ou seja, basta ir a **módulos > gerir e instalar módulos** e procurar por “Walking Time”. No entanto, como o plugin é experimental, poderá terá de activar no separador **configurações** a opção **Mostrar também módulos experimentais**.