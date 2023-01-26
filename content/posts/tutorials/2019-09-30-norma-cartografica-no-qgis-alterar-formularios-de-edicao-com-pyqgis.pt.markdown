---
date: 2019-09-30 21:06:06+00:00
title: Norma Cartográfica no QGIS - Alterar formulários de edição com PyQGIS
tags:
- pyqgis
- QGIS
- Recart
hero: /images/posts_hero/form_widget_pyqgis.png
---

Enquanto preparava um projecto QGIS para leitura da estrutura de base de dados descrita nas novas [Normas e Especificações Técnicas de Cartografia ](http://www.dgterritorio.pt/cartografia_e_geodesia/cartografia/normas_e_especificacoes_tecnicas_de_cartografia/), comecei a configurar os formulários de edição das várias camadas de forma a:



	  1. Bloquear a edição de campos só de leitura, como por exemplo um identificador.
	  2. Configurar widgets adequados aos campos, que facilitem a vida do utilizador e evitem que cometa erros, como por exemplo campos com dadas e listas de valores fixos.

No fundo, o que procurava era qualquer coisa deste género:

![Peek 2019-09-30 15-04_2](/images/2019/09/peek-2019-09-30-15-04_2.gif)


Antes de mais, é preciso dizer que o QGIS, quando lê uma tabela PostGreSQL/PostGIS, já faz um excelente trabalho a adivinhar, para cada campo, o tipo de widget a usar, assim  como as constraints a aplicar. O que é uma enorme ajuda. No entanto, alguns campos precisam de uma configuração extra.

Se se tratassem de meia-dúzia de camadas e campos, teria feito tudo de manualmente, mas ao fim da quinta camada, o meu Mantra começou a chamar por mim:


<blockquote>"Quando usas um computador, se estás a fazer manualmente uma tarefa repetitiva, estás a fazê-la mal!"</blockquote>


Então, comecei a pensar como poderia fazer esta configuração de forma mais sistemática para todas as camadas e campos, sem me causar tendinites. Depois de alguma pesquisa, cheguei às funções PyQGIS que apresento a seguir.


## Tornar um campo apenas  de leitura


O campo identificador é gerado automaticamente pela base de dados, pelo que o utilizador não só não precisa de o editar, como não deve. Por essa razão, convém tornar o campo não editável.

![Layer Properties - cabo_electrico | Attributes Form_103](/images/2019/09/layer-properties-cabo_electrico-attributes-form_103.png)


Para o fazer programaticamente recorri ao seguinte código.


    def field_readonly(layer, fieldname, option = True):
        fields = layer.fields()
        field_idx = fields.indexOf(fieldname)
        if field_idx >= 0:
            form_config = layer.editFormConfig()
            form_config.setReadOnly(field_idx, option)
            layer.setEditFormConfig(form_config)

    # Exemplo para o campo "identificador"

    project = QgsProject.instance()
    layers = project.mapLayers()

    for layer in layers.values():
        field_readonly(layer,'identificador')





## Configurar um campo com o widget DateTime


Os campos de datas ficam configurados automaticamente, mas o widget usado por omissão, ao contrário do que é exigido pela norma, apenas guarda a data e não a data e hora. Para além disso, para o meu caso posso preencher o campo da data com a data e hora actuais, para evitar ter de o fazer de forma manual. 

Comecei por configurar como queria um campo de exemplo e depois fui ver como a configuração era gravada em PyQGIS usando a consola python:


    >>>layer = iface.mapCanvas().currentLayer()
    >>>layer.fields().indexOf('inicio_objeto')
    1
    >>>field = layer.fields()[1]
    >>>field.editorWidgetSetup().type()
    'DateTime'
    >>>field.editorWidgetSetup().config()
    {'allow_null': True, 'calendar_popup': True, 'display_format': 'yyyy-MM-dd HH:mm:ss', 'field_format': 'yyyy-MM-dd HH:mm:ss', 'field_iso_format': False}



Com isso consegui criar uma função que me permitisse configurar qualquer campo com a mesma configuração. 

**ACTUALIZAÇÃO:** Como extra, usei a função `now()` como default para quando um novo elemento é criado.


    def field_to_datetime(layer, fieldname):
        config = {'allow_null': True,
                  'calendar_popup': True,
                  'display_format': 'yyyy-MM-dd HH:mm:ss',
                  'field_format': 'yyyy-MM-dd HH:mm:ss',
                  'field_iso_format': False}
        type = 'Datetime'
        fields = layer.fields()
        field_idx = fields.indexOf(fieldname)
        if field_idx >= 0:
            widget_setup = QgsEditorWidgetSetup(type,config)
            layer.setEditorWidgetSetup(field_idx, widget_setup)
	    layer.setDefaultValueDefinition(field_idx, QgsDefaultValue('now()'))


    # Exemplo para os campos "inicio_objeto" e "fim_objeto"

    for layer in layers.values():
        field_to_datetime(layer,'inicio_objeto')





## **Configurar um campo com o widget Value Relation**


No modelo de dados, muitas tabelas contém campos que apenas aceitam um conjunto finito de valores. Valores estes que são listados noutra tabela, os chamados _Foreign keys_.

Para estes casos, é conveniente no QGIS configurar um widget de relação de tabela. Para o fazer de forma programática, o processo é identico ao mostrado anteriormente, em que há que descobrir primeiro o tipo e a configuração de uma campo já preparado. Mas neste caso, cada campo terá uma configuração ligeiramente diferente.

Felizmente, quem desenhou a estrutura de dados facilitou-nos a vida ao dar o mesmo nome aos campos e às tabela de valores associada, e todos eles começados com a texto "valor_", tornando possivel que também essa parte seja automática.

A funçao abaixo começa por identificar para determinada camada todos os campos cujo nome começa por "valor_". Depois iterando sobre os campos encontrados, adapta a configuração de forma a usar como camada de referência ('Layer') a camada com o mesmo nome que o campo.


    def field_to_value_relation(layer):
        fields = layer.fields()
        pattern = re.compile(r'^valor_')
        fields_valor = [field for field in fields if pattern.match(field.name())]
        if len(fields_valor) > 0:
            config = {'AllowMulti': False,
                      'AllowNull': True,
                      'FilterExpression': '',
                      'Key': 'identificador',
                      'Layer': '',
                      'NofColumns': 1,
                      'OrderByValue': False,
                      'UseCompleter': False,
                       'Value': 'descricao'}
            for field in fields_valor:
                field_idx = fields.indexOf(field.name())
                if field_idx >= 0:
                    print(field)
                    try:
                        target_layer = QgsProject.instance().mapLayersByName(field.name())[0]
                        config['Layer'] = target_layer.id()
                        widget_setup = QgsEditorWidgetSetup('ValueRelation',config)
                        layer.setEditorWidgetSetup(field_idx, widget_setup)
                    except:
                        pass
                else:
                    return False
        else:
            return False
        return True

    # Correr função em todas as camadas
    for layer in layers.values():
        field_to_value_relation(layer)





## **Conclusão**


Assim, de forma relativamente rápida, consegui configurar todas as camadas do projecto com os widgets que queria.

![Peek 2019-09-30 16-06](/images/2019/09/peek-2019-09-30-16-06.gif)

Pode consultar o código completo [aqui](https://gist.github.com/SrNetoChan/6e4bec315749e3d65e3b7c91bb0a98ad)

Esta é a ponta do iceberg. Havendo necessidade, com um pouco de paciência e pesquisa, outras configurações podem ser alteradas usando PyQGIS. Por isso, pense nisso antes de começar a configurar camada a camada, campo a campo.
