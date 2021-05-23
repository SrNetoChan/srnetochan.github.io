---

date: 2016-01-28 21:52:54+00:00
title: Saudades do QGIS (enquanto uso ArcGIS)
tags:
- Opinião
- QGIS
---

## (aka Funcionalidades que os utilizadores de ArcGIS Desktop nem sonham que existem)


De tempos a tempos, leio artigos de comparação entre o ArcGIS e o QGIS. Uma vez que partem geralmente do ponto de vista de utilizadores de ArcGIS, acabam invariavelmente em observações parciais sobre a falta de funcionalidades do QGIS. Está na hora de mudar o ponto de vista. Por isso, convido-vos a acompanharem-me neste artigo (um pouco) longo, **totalmente e assumidamente parcial**.


<blockquote>"Olá, o meu nome é Alexandre, e tenho usado... [QGIS](http://www.qgis.org)"</blockquote>


Eis algo que eu diria numa sessão de terapia em grupo dos Utilizadores Anónimos do QGIS. Estou a precisar de ir a uma sessão dessas porque, tendo sido recentemente forçado a voltar a usar - de forma temporária - o ArcGIS, sinto muita muita muita falta do QGIS em vários aspectos.

Em tempos idos, houve alturas em que usava o ArcGIS diariamente. Usei-o até à versão 9.3.1, até que me decidi a mudar para o QGIS (versão 1.7.4, acho eu). Na altura, senti falta de algumas (muitas?) funcionalidades do ArcGIS, mas estava disposto a trocá-las pela liberdade oferecida pela filosofia [Open Source](https://en.wikipedia.org/wiki/Open_source). Desde essa altura, passou-se muita coisa no universo QGIS, e eu tenho-me mantido avidamente atento à sua evolução. Esperaria que o mesmo tivesse acontecido no lado do ArcGIS Desktop, mas, ao que me parece, isso não aconteceu.

Estou a utilizar o topo de gama da ESRI, o ArcGIS 10.3, licença advanced, e debato-me para conseguir fazer pequenas coisas que são simplesmente inexistentes em ArcGIS.  Assim, o que se segue é uma lista de funcionalidades do QGIS das quais sinto falta.

**Aviso:** Para aqueles que usam exclusivamente o ArcGIS, algumas destas funcionalidades podem apanhá-los de surpresa.


## Controlo de transparência




<blockquote>"O ArcGIS tem transparência! Está no separador _Display_, nas propriedades da camada!"</blockquote>


Sim, é verdade, mas... apenas é possível configurar transparência ao nível da camada. Ou seja, ou é tudo transparente, ou não é nada...

No QGIS, é possível determinar a transparência ao nível da camada, ao nível do  elemento/símbolo, e ao nível da cor. Podem achar que estou a sobrevalorizar o assunto, mas vejam a diferença nas imagens abaixo.

![Transparencia_camada](/images/2016/01/transparencia_camada.png)
![Transparencia_elemento](/images/2016/01/transparencia_elemento1.png)
![Transparencia_cor](/images/2016/01/transparencia_cor.png)


Reparem que no QGIS é possível controlar a transparência sempre (ou quase sempre) que se define uma cor. Isto inclui em anotações (como as usadas nas imagens acima), em etiquetas, e em itens do compositor de impressão. É até possível determinar a transparência de uma cor usando a função RGBA() numa expressão! Que mais se pode pedir? :-)

![Screenshot from 2016-01-27 14:12:34](/images/2016/01/screenshot-from-2016-01-27-141234.png)



## Modos de Blending


Esta funcionalidade é uma das preciosidades do QGIS, a possibilidade de combinar camadas como faríamos na maioria dos software de edição de imagem. Ao nível da camada e/ou elemento, é possível controlar como o mesmo irá interagir com os elementos e camadas abaixo. Para além do modo normal, estão disponíveis mais 12 modos: _Lighen_, _Screen_, _Dodge_, _Darken_, _Multiply_, _Burn_, _Overlay_, _Soft light_, _Hard light_, _Difference_ and _Subtract_. Não me vou alongar sobre as propriedade de cada um. Vejam esta [página](https://en.wikipedia.org/wiki/Blend_modes) para se informarem acerca da matemática por detrás de cada um deles e alguns [exemplos](http://image.slidesharecdn.com/blendmodesforopengl-140213092122-phpapp02/95/blend-modes-for-opengl-3-638.jpg?cb=1392283377).

Sem se experimentar um pouco, não é fácil perceber em que é que esta funcionalidade nos pode ser útil à produção cartográfica. Eu tive a oportunidade de o fazer enquanto tentava responder a [esta pergunta](http://gis.stackexchange.com/a/82815/6191).

![2wph4](/images/2016/01/2wph4.jpg)


Uma das mais comuns utilizações para o _blending_ é quando queremos realçar ou simular o relevo adicionando um _hillshade_ por cima das restantes camadas. Em ArcGIS, apenas é possível controlar a transparência da camada, e o resultado final fica sempre um pouco esbatido em relação ao original. Mas no QGIS, é possível manter a força das cores originais usando o modo _multiply_ na camada do _hillshade_.

[caption id="attachment_1809" align="alignnone" width="1269"]![Screenshot from 2016-01-27 15:24:38](/images/2016/01/screenshot-from-2016-01-27-152438.png)
Hipsometria com as cores originais[/caption]

[caption id="attachment_1806" align="alignnone" width="1269"]![Screenshot from 2016-01-27 15:25:45](/images/2016/01/screenshot-from-2016-01-27-152545.png)
Cores da hipsometria esbatidas pelo _hillshade_ transparente[/caption]

[caption id="attachment_1805" align="alignnone" width="1269"]![Screenshot from 2016-01-27 15:24:45](/images/2016/01/screenshot-from-2016-01-27-152445.png)
Cores originais da hipsometria com o _hillshade_ usando o _multiply_ do QGIS[/caption]

É também possível usar os modos de _blending_ em elementos do compositor de mapas, permitindo combiná-los com outros elementos e texturas. Isto dá-nos a oportunidade de obter resultados [mais "artísticos"](/images/2014/04/14/mapa-envelhecido-aged-map/) sem a necessidade de pós-processamento num software de edição de imagem.


## Configuração de cores


O eficiente controlo das cores é algo essencial para um cartógrafo, e o QGIS permite-nos controlá-las como profissionais que somos. É possível escolher as cores usando diferentes menus. Menus que poderá reconhecer de software como o Inkscape, Photoshop, Gimp, etc...

[gallery ids="991,988,989" type="rectangular"]

O meu favorito é o _color picker_. Ora vejam, usando o _color picker_, é possível recolhermos cores de qualquer sítio do nosso ecrã, fora ou dentro do QGIS. Algo muito útil e produtivo quando queremos usar uma cor já existente no nosso mapa, da legenda, de uma palete do  [COLOURlovers](http://www.colourlovers.com/) ou do logo de uma empresa.

[caption id="attachment_1571" align="alignnone" width="862"]![anim](/images/2016/01/anim.gif)
Recollhendo uma cor fora do QGIS[/caption]

Também podemos fazer _copy/paste_ de cores entre menus, gravar e importar paletes de cores e até dar nome a uma cor e [usá-la numa variável](http://nyalldawson.net/2015/12/exploring-variables-in-qgis-pt-2-project-management/). Com tudo isto disponível, é-me difícil engolir o menu de selecção de cores do Windows. :(

[gallery ids="992,990" type="columns"]



[gallery ids=&quot;1555,1554&quot; type=&quot;rectangular&quot; orderby=&quot;rand&quot;]


## Modos "avançados" de simbologia de vectores


No ArcGIS, existem várias maneiras de simbolizar as camadas de vectores. Temos _Single symbol_, _Unique values_, _Unique values many fields_... e por aí fora. À primeira impressão, pode até parecer que ao QGIS faltam alguns destes modos, mas acreditem em mim, não faltam! Na verdade, o QGIS oferece muito mais flexibilidade no que toca a simbolizar as suas camadas.

Para começar, pode-se usar tanto 'campos' como 'expressões' em qualquer um dos modos de simbologia, enquanto que no ArcGIS apenas é possível usar 'campos'. Alimentado por centenas de funções e com a possibilidade de criarmos as nossas próprias funções usando Python, o que é possível conseguir-se com expressões não tem limites. Torna-se possível seleccionar, recalcular, normalizar (etc...) um número infinito de campos para criar os nossos próprios "valores" (sem falar de que é possível aprimorar as etiquetas associadas aos valores para criar a legenda ideal).

[caption id="attachment_1580" align="alignnone" width="825"]![Screenshot from 2016-01-20 22:34:54](/images/2016/01/screenshot-from-2016-01-20-223454.png)
Símbolos graduados no QGIS usando uma expressão para calcular a densidade populacional[/caption]

E depois, no QGIS existem alguns modos "especiais" (e de certa forma bastante específicos) de simbologia, que nos fazem exclamar "wooooh". Como, por exemplo, os **polígonos invertidos**, que permitem preencher o exterior dos polígonos (bom para mascarar outros elementos, os **pontos desfasados**, para mostrar pontos fisicamente demasiado próximos para serem representados, e o **_Heatmap_** que transforma qualquer camada de pontos num _heatmap_ sem necessidade de conversão para _raster_ e que é automaticamente actualizado sempre que editamos a camada de pontos.

[caption id="attachment_1583" align="alignnone" width="777"]![Screenshot from 2016-01-20 22:58:44](/images/2016/01/screenshot-from-2016-01-20-225844.png)
Polígonos invertidos a mascarar o exterior de uma área de interesse[/caption]

Mas deixei o melhor para o fim. O "_One Renderer to rule them all_", a simbologia **baseada em regras**. Com este modo, é possível adicionar várias regras, agrupá-las numa estrutura de árvore, e atribuir-lhes um símbolo distinto. Cada elemento irá ser representado consoante cumpre ou não cada uma das regras. Isto dá aos utilizadores de QGIS controlo absoluto sobre a simbologia das suas camadas e que, em conjunto com o editor de expressões e as _data-defined properties_, abre a porta às mais diversas aplicações (veja alguns exemplos na secção abaixo).

[caption id="attachment_1589" align="alignnone" width="869"]![rulesymbol_ng_line](/images/2016/01/rulesymbol_ng_line.png)
Simbologia por regras[/caption]


## Atlas


Uma das minhas funcionalidade favoritas do QGIS é o Atlas do compositor de impressão. Eu sei que o ArcGIS tem o seu próprio "Atlas", as _Data Driven Pages_, mas sinceramente, não é a mesma coisa.

Penso que conhecem o funcionamento básico destas ferramentas em ambos os _softwares_. Cria-se um _layout_ de um mapa, escolhe-se uma camada de vectores como _coverage_ e software irá criar um mapa, devidamente centrado e/ou aproximado para cada elemento da camada. É também possível adicionar etiquetas que irão mudar de acordo com os valores guardados nos atributos da camada.

**Mas no QGIS as funcionalidades vão um pouco mais além...**

Basicamente, podemos usar os atributos e geometria dos elementos da camada onde quer que seja possível usar uma expressão e, **no QGIS, as expressões estão por todo o lado**. Desta forma, a maioria das propriedades tanto de camadas, como dos elementos do mapa podem ser controlados pela camada usada no atlas.

Com a devida configuração, iterando por todos os elementos da camada de atlas, é possível [escolher os elementos de outras camadas a mostrar ou a esconder](http://nathanw.net/2013/12/02/waiting-for-qgis-2-2-highlighting-current-atlas-feature/), [alterar a cor de base do seu mapa](http://nathanw.net/2014/09/23/qgis-atlas-on-non-geometry-tables/), [rodar e redimensionar as páginas de acordo com as dimensões do elemento](/images/2014/11/09/series-de-mapas-com-formatos-multiplos-em-qgis-2-6-parte-1-multiple-format-map-series-using-qgis-2-6-part-1/), [escolher um logo específico para acompanhar cada mapa](http://nyalldawson.net/2013/04/a-neat-trick-in-qgis-2-0-images-in-atlas-prints/), e por aí fora. Mais uma vez, o céu é o limite.

[caption id="attachment_535" align="aligncenter" width="506"]![mosaico_regioes_fixed](/images/2014/11/mosaico_regioes_fixed.png)
Série de mapas cuja dimensão foi automaticamente alterada para cobrir os elementos a uma escala fixa[/caption]

Por isso, se se aliar a funcionalidade de **Atlas** com as **_data-defined properties_**, a **simbologia por regras** e as **expressões**, não me parece que o _Data Driven Pages_ do ArcGIS seja um rival à altura. Discordam? Então tentem responder a [esta questão](http://gis.stackexchange.com/questions/174817/feature-label-visibility-based-on-spatial-relationship-to-index-feature-using-da?atw=1).

**Dica: **Se realmente quiserem levar a produção de cartografia a outro nível de automatismo, usando bases de dados como Spatialite ou Postgis, é possível criar camadas de _coverage_ adequadas para as vossas necessidades através de _views_. Acaba-se a redundância e a camada estará sempre actualizada.


## Menus de estilo e etiquetas


Este é um caso mais de experiência do utilizador (UX) do que propriamente uma funcionalidade em falta, mas não imaginam como é confortável ter todas as opções das etiquetas e dos estilos em apenas um par de janelas (com vários separadores, claro).

Quando uso as opções de simbologia do ArcGIS parece que estou no filme "[A origem (Inception)](http://www.imdb.com/title/tt1375666/)", às tantas, já nem sei onde estou! Por exemplo, para adicionar um rebordo tracejado a um símbolo de uma camda de polígonos, é preciso abrir 5 janelas diferentes, e depois voltar para trás a clicar OK, OK, OK...

[caption id="attachment_1244" align="aligncenter" width="1499"]![Capture](/images/2016/01/capture.jpg)
Opções de símbolos do ArcGIS[/caption]

No QGIS, uma vez aberta a janela de propriedades da camada, todas as opções estão a um clique de distância (ou quase). E basta carregar em OK ou Aplicar uma vez para visualizar o resultado!

[caption id="attachment_1561" align="alignnone" width="907"]![Screenshot from 2016-01-20 21:51:33](/images/2016/01/screenshot-from-2016-01-20-215133.png)
Opções de estilos do QGIS[/caption]

Como bónus, é possível fazer _copy/paste_ de uma camada para a outra, tornando a configuração do estilo de várias camadas muito mais rápida. Ao que me respondem:


<blockquote>"Não sejas ridículo! O ArcGIS também permite importar símbolos de outras camadas."</blockquote>


Símbolos? Sim. Etiquetas? Não! E se, como eu, perdem algum tempo a configurar de forma primorosa as etiquetas de uma camada, ter de fazer o mesmo ou semelhante para outras camadas, vai-vos dar vontade de chorar... A mim dá.

(Vou deixar a comparação de múltiplos estilos por camada do QGIS vs Data Frames do ArcGIS para outra altura)


## WFS




<blockquote>"O quê?!!"</blockquote>


Yup, é isso mesmo, o ArcGIS não suporta o [standard OGC WFS](http://www.opengeospatial.org/standards/wfs) a não ser que se compre uma extensão extra: A Extensão de [Data Interoperability](http://www.esri.com/software/arcgis/extensions/datainteroperability/pricing).

Com o universo SIG (e não só) a evoluir cada vez mais para Dados Abertos, Normas Abertas e Serviços Web OGC, esta situação revela uma posição extremamente mercantil por parte da ESRI. Se fosse um cliente ESRI, sentir-me-ia aldrabado. <sarcasmo> Ou talvez não... talvez me sentisse grato por mais uma oportunidade de investir algum dinheiro nas suas funcionalidades avançadas...<\sarcasmo>

No QGIS, como tudo o resto, o uso do WFS é livre. Tudo o que é preciso é adicionar um URL para o servidor WFS, e podemos começar a adicionar as camadas disponibilizadas, com a certeza de que estarão devidamente actualizadas pela entidade responsável pelo serviço.

![Screenshot from 2016-01-20 21:58:54](/images/2016/01/screenshot-from-2016-01-20-215854.png)



Felizmente, para os utilizadores ArcGIS menos afortunados, existe sempre a "cómoda" possibilidade de fazerem o download das camadas através do browser de internet :-P.





    http://giswebservices.massgis.state.ma.us/geoserver/wfs?request=GetFeature&service=wfs&version=1.0.0&typename=massgis:GISDATA.TOWNS_POLY&outputformat=SHAPE-ZIP




Ou então podem sempre usar o QGIS (ou outro open soure qualquer) para fazer o download. Mas não se esqueçam que as camadas não se irão actualizar sozinhas.





## Editor de expressões




Já fiz menção às expressões várias vezes, mas para aqueles que desconhecem o editor de expressões, decidi terminar este artigo com umas das minhas funcionalidades favoritas.




Não conheço o suficiente do editor de expressões do ArcGIS para o poder criticar. Tanto quando percebo, podemos usá-lo para criar _labels_ e para preencher um campo usando o _field calculator_. Sei que existem certamente muitas funções que podemos usar (apenas utilizei algumas) mas não são visíveis ao utilizador comum. Provavelmente é preciso consultar a documentação de ajuda para conhecê-las todas. É ainda possível criar funções em VBScript, Python e JsScript.


![Capture](/images/2016/01/capture2.jpg)



No QGIS, como já referi, podem-se usar expressões praticamente em todo o lado, o que é bastante conveniente para muitas aplicações. No que toca a funções, existem centenas disponíveis directamente na janela do editor de expressões, todas devidamente acompanhadas por informação sobre a sua sintaxe e alguns exemplos ilustrativos. Também se podem usar campos e valores como no ArcGIS, e até existe uma secção de "expressões recentes" para quando precisamos de reutilizar uma expressão.


![Capture](/images/2016/01/capture3.jpg)


Para além disso, também é possível criar as nossas próprias funções em Python (nada de VBScript ou JsScript), mas desta feita num editor próprio, num outro separador. Um editor equipado com _autocomplete_ e _code highlight_ para nos facilitar a vida, e que permite gravar as funções no ambiente do utilizador para serem usadas posteriormente (inclusive noutras sessões de QGIS).

![Capture](/images/2016/01/capture4.jpg)



## Conclusão


Estas não são certamente as únicas funcionalidades do QGIS de que sinto falta, e não serão certamente as mais limitantes (por exemplo, não poder usar em pleno bases de dados Spatialite e Postgis vai, de certeza, tornar-me a vida num inferno nos próximos tempos), mas são aquelas que identifiquei assim que (re)abri o ArcGIS pelas primeiras vezes.

Para além disso, sinto que, com a  actual dinâmica de desenvolvimento do QGIS, a cada nova versão, esta lista irá crescer muito rapidamente. Embora ainda não tenha experimentado o ArcGIS Pro, na minha opinião, não me parece que a ESRI consiga acompanhar o ritmo.

"Ainda há coisas que sente falta do ArcGIS?" Claro que sim. Por exemplo, sinto falta de suporte para CMYK durante a exportação de mapas, mas não tanto como sinto falta do QGIS neste momento. Para além disso, sei que essas lacunas serão resolvidas mais cedo ou mais tarde.

No fundo, até gostei da oportunidade de voltar ao ArcGIS, pois permitiu-me reforçar a minha opinião acerca do QGIS. Tem tudo a ver com liberdade! Não só a liberdade de usar o programa quando e para o que bem entender (algo que para mim já era ponto assente), mas também a liberdade de controlar o programa em si e os seus _outputs_. Mantendo a facilidade de utilização para recém chegados e principiantes, muito foi feito para facilitar a vida de utilizadores experientes, e eles ficam eternamente agradecidos por isso (pelo menos eu fico).


<blockquote>

>
> Dito isto, The winner is... QGIS!!
>
>
</blockquote>




### O Fim




#### (de um artigo extremamente parcial)
