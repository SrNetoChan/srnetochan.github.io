---

date: 2013-05-29 22:05:18+00:00
title: Substituir strings na tabela de atributos do QGIS
tags:
- QGIS
---

Hoje, ao rever uma camada vectorial de distribuição de fauna com interesse para a conservação com a nossa bióloga de serviço, Sara Saraiva, tive necessidade de corrigir (em todas as linhas de determinado atributo) o nome "Aquila fasciatus", substituindo-o por "Aquila fasciata".

Devido à opção tomada na organização dos dados, cada polígono continha uma listagem de espécies que nele ocorrem, e o nome a corrigir encontrava-se no meio da mesma. A correcção teria de ser feita sem alterar os restantes nomes.

[![Screenshot from 2013-05-29 19:44:20](images/2013/05/screenshot-from-2013-05-29-1944201.png)
](images/2013/05/screenshot-from-2013-05-29-1944201.png)

Tratavam-se de cerca de 80 linhas, e na verdade o termo "Aquila fasciatus" parecia uma meia dúzia de vezes, podendo ser facilmente substituído manualmente. No entanto, a minha honra geek não me permitia efectuar tal processo repetitivo e interrogava-se: "E se fossem mais?".

Tinha portanto de encontrar uma forma de o fazer automaticamente. Precisava de um género de "Localizar e substituir...", funcionalidade muito comum em programas de edição de texto e folhas de calculo, e sabia que o QGIS não me iria deixar ficar mal.

Depois de alguma pesquisa, a solução foi encontrada na calculadora de campo, usando a função **replace()**.

[![Screenshot from 2013-05-29 22:08:41](images/2013/05/screenshot-from-2013-05-29-220841.png?w=584)
](images/2013/05/screenshot-from-2013-05-29-220841.png)

A expressão é:


    replace("campo",'string_antiga','string_nova')


E o resultado foi o esperado.

[![Screenshot from 2013-05-29 22:14:37](images/2013/05/screenshot-from-2013-05-29-221437.png)
](images/2013/05/screenshot-from-2013-05-29-221437.png)
