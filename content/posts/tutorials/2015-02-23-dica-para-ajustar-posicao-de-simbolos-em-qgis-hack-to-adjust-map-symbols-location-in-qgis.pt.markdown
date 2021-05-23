---

date: 2015-02-23 23:44:33+00:00
title: Dica para ajustar posição de símbolos em QGIS
tags:
- Cartografia
- Dica
- QGIS
---

De quando em vez aparecem-me zonas com demasiado símbolos no mesmo local, e pensei como seria fantástico se os pudesse arrastar para um local mais conveniente sem ter de alterar as suas geometrias, tal como é possível fazer com as etiquetas. Esse pensamento deu-me a ideia base para a dica que vou demonstrar.

Escolha a sua camada de pontos e comece por criar dois novos campos chamados symbX e symbY (Tipo: Decimal; Tamanho: 20; precisão: 5). No separador "Estilo" das propriedades da camada, defina para **cada nível do seu símbolo** o seguinte: Escolher "unidade do mapa" como a unidade para as opções de afastamento; Usar a seguinte expressão na opção afastamento das propriedades definidas por dados.

[code]

CASE WHEN symbX IS NOT NULL AND symbY IS NOT NULL THEN
    tostring($x - symbX) + ',' + tostring($y - symbY)
ELSE
    '0,0'
END

[/code]

[![Screenshot from 2015-02-22 18:18:43](/images/2015/02/screenshot-from-2015-02-22-181843.png)
](/images/2015/02/screenshot-from-2015-02-22-181843.png)

Tenha atenção que, se as coordenadas do seu mapa tiver valores negativos, será necessário uma pequena alteração ao código. E. g., se tiver valores negativos em X deverá usar-se  antes a expressão "tostring(symbX -$x)".

De forma temporária coloque etiquetas na sua camada usando um texto pequeno (eu usei o '+' (sinal de mais) centrado e com um buffer branco) e defina as coordenadas X e Y dos propriedades definidadas por dados usando os campos symbX e symbY,

[![Screenshot from 2015-02-22 22:42:07](/images/2015/02/screenshot-from-2015-02-22-224207.png?w=660)
](/images/2015/02/screenshot-from-2015-02-22-224207.png)

A partir desse momento, quando usar a ferramenta de mover etiquetas, não só alterará a posição da etiqueta, mas também a do próprio símbolo! Fantástico, não?

[![anim](/images/2015/02/anim.gif)
](/images/2015/02/anim.gif)

Note que as geometria dos elementos não são alteradas durante o processo. Para além disso, lembre-se que neste caso também poderá [adicionar linhas de guia](/images/2015/01/12/etiquetas-com-guias-em-qgis-e-postgis-labels-leading-lines-with-qgis-and-postgis/) para ligar os símbolos à posição original do ponto.
