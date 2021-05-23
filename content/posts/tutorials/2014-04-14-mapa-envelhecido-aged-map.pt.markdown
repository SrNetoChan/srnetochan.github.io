---

date: 2014-04-14 13:35:11+00:00
title: Old map in QGIS
tags:
- QGIS
---

Inspirado [num artigo](http://anitagraser.com/2013/07/29/vintage-map-design-using-qgis/) da Anita Graser, tentei usar o [QGIS](http://www.qgis.org/pt_PT/site/) para criar um mapa de [Cascais](http://www.openstreetmap.org/#map=16/38.6967/-9.4156) que tivesse um aspecto antigo, como que se tivesse sido metodicamente desenhado à mão, embora tivesse ligeiramente maltratado.





## Definir os Estilos




Comecei por definir a simbologia para cada um dos elementos a representar.





### **Edifícios**




Para preenchimento dos edifícios tentei usar uma cor que lembrasse os [telhados portugueses](http://olhares.sapo.pt/client/files/foto/big/517/5174082.jpg), e muito usada em mapas antigos de cidades, com um contorno ligeiramente mais escuro do mesma cor.




Para dar dimensão aos edifícios criei uma sombra por baixo, adicionando um "_simple fill_" em tons escuros e usando a opção Offset X,Y. Os valores escolhidos tiveram em conta a direcção predominante das fachadas dos edíficios de forma a que o efeito fosse visível por toda a área do mapa.


[![Capturar_4](/images/2014/04/capturar_4.png)
](/images/2014/04/capturar_4.png)


# [![Capturar_6](/images/2014/04/capturar_6.png)
](/images/2014/04/capturar_6.png)




### Espaços verdes




Para espaços verdes, usei 3 camadas de simbologia. Uma base com o preenchimento a verde. Uma segunda camada com um contorno grosso ligeiramente mais escuro, e com uma [funcionalidade](http://changelog.linfiniti.com/qgis/version/21/#115) que surgiu na versão 2.2 e que permite mostrar as linhas de contorno apenas no interior do polígono. Para tal é necessário escolher o tipo "outline: simple line" e seleccionar a opção "draw line only inside polygon".




[![Capturar_5](/images/2014/04/capturar_5.png)
](/images/2014/04/capturar_5.png)




.A última camada de simbologia é uma linha fina num verde mais escuro que as restantes.




[![Capturar_7](/images/2014/04/capturar_7.png)
](/images/2014/04/capturar_7.png)





### O Mar




Para o mar usei a mesma técnica que para os espaços verdes, mas em tons de azul e com o contorno do meio mais exagerado.




[![Capturar_8](/images/2014/04/capturar_8.png)
](/images/2014/04/capturar_8.png)





###  Estradas




Para símbolo das estradas usei uma linha grossa com um tom pastel alaranjado. Criei também etiquetas dos nomes das ruas ao longo das linhas usando uma fonte script (no meu caso o [Pristina Bold](http://ufonts.com/fonts/pristina.html)). Para melhorar a legibilidade adicionei um pequeno buffer branco com 50% de transparência.




[![Captura de tela 2014-04-11 17.55.04](/images/2014/04/captura-de-tela-2014-04-11-17-55-04.png)
](/images/2014/04/captura-de-tela-2014-04-11-17-55-04.png)




[![Capturar_9](/images/2014/04/capturar_9.png)
](/images/2014/04/capturar_9.png)





### Praia




Nas praias, para além da base, usei um point pattern fill, com um círculo bastante pequeno.




[![Capturar_11](/images/2014/04/capturar_11.png)
](/images/2014/04/capturar_11.png)[![Capturar_10](/images/2014/04/capturar_10.png)
](/images/2014/04/capturar_10.png)





## Composição do mapa




Embora o aspecto do mapa não esteja muito longe do resultado final, é no _Print Composer_ que se dão os toques finais. Em primeiro lugar, comecei por preencher toda a folha com a imagem de uma textura de [papel antigo](http://lostandtaken.com/gallery/antique7.html) (aliás, o mesmo usado pela Anita no seu artigo). Para o efeito não ficar demasiado pesado, apliquei uma transparência de 20% à imagem.




[![Captura de tela 2014-04-14 11.24.53](/images/2014/04/captura-de-tela-2014-04-14-11-24-53.png)
](/images/2014/04/captura-de-tela-2014-04-14-11-24-53.png)




Depois adiciona-se o mapa propriamente dito e nas suas propriedades alteramos o modo de _rendering_ de "_normal_" (usado por defeito) para "_multiply_". Desta forma parece que o mapa foi desenhado directamente sobre o papel antigo.




[![Captura de tela 2014-04-14 11.30.07](/images/2014/04/captura-de-tela-2014-04-14-11-30-07.png)
](/images/2014/04/captura-de-tela-2014-04-14-11-30-07.png)




Depois é uma questão de adicionar mais umas etiquetas (nomes de praias e locais), uma rosa dos ventos e uma escala gráfica (usando sempre o modo de rendering "multiply" para parecer que foi desenhado por cima da folha), e... Voilá, temos mapa!




[![mapa_antigo](/images/2014/04/mapa_antigo.jpg?w=584)
](/images/2014/04/mapa_antigo.jpg)



