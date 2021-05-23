---

date: 2014-03-25 08:41:42+00:00
title: Novo plugin QGIS "Walking time"
---

Finalmente "terminei" o meu novo plugin. Coloquei o termo entre aspas porque creio que ainda há espaço para alguma melhorias. Este plugin surgiu da necessidade de estimar o tempo de percurso das pequenas e grandes rotas de cascais, e começou como um pequeno script em python. Depois decidi criar um interface gráfico e publicá-lo como plugin porque talvez seja útil a mais pessoas.




[![icon_large](images/2014/03/icon_large.png?w=150)
](images/2014/03/icon_large.png)




O **Walking time** é um plugin python para QGIS que usa a [Tobbler's hiking function](https://en.wikipedia.org/wiki/Tobler's_hiking_function) para estimar o tempo de percurso ao longo de uma linha consoante o declive.




Os dados de input necessários são uma camada vectorial de linhas e uma camada raster com valores de elevação (1). É possível ajustar a velocidade base (em terreno plano) de acordo com o tipo de caminhada ou caminhante. Por defeito, o valor usado é de 5 km\h (2). O plugin actualiza ou cria campos com o tempo estimado em minutos, no sentido directo e no sentido inverso (3). É possível correr o plugin para todos os elementos da camada vectorial, ou apenas nos percursos seleccionados (4).




O plugin pode também ser usado para preparar uma rede ([grafo](https://pt.wikipedia.org/wiki/Teoria_dos_grafos)) para realizar análise de redes onde se queira usar como custo o tempo de percurso.




[![Captura de tela 2014-03-24 12.12.17-01](images/2014/03/captura-de-tela-2014-03-24-12-12-17-01.png)
](images/2014/03/captura-de-tela-2014-03-24-12-12-17-01.png)


Repositório QGIS: [http://plugins.qgis.org/plugins/walkingtime/](http://plugins.qgis.org/plugins/walkingtime/)

Código: [https://github.com/SrNetoChan/WalkingTime](https://github.com/SrNetoChan/WalkingTime)

Reportar bugs | Bug report:[ https://github.com/SrNetoChan/WalkingTime/issues](https://github.com/SrNetoChan/WalkingTime/issues)
