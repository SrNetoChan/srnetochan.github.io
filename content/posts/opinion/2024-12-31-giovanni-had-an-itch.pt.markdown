---
title: Algo Inquietava o Giovanni... um Conto Sobre Desenvolvimento em Open Source
date: 2024-12-31
menu:
  sidebar:
    name: Algo Inquietava o Giovanni...
    identifier: giovanni-tinha_uma_comichao
    parent: opinion-articles
    weight: 20
tags:
- QGIS
- Open Source
hero: /images/posts_hero/duplicate_layout_grid.png
---

Era uma vez um homem chamado Giovanni (um nome totalmente fictício, de forma alguma relacionado com o CEO da [NaturalGIS](http://naturalgis.pt) e defensor de Open Source, [Giovanni Manghi](https://www.linkedin.com/in/giovannimanghi/)). Era um *poweruser* diário do QGIS e adorava o software, mas tinha uma inquietação... Algo o chateava. Como qualquer outro protagonista principal dos contos tradicionais, em vez de olhar para o lado, decidiu aceitar a missão e resolvê-la.

Esta inquietação estava relacionada com as grelhas de layout do [QGIS](www.qgis.org). Giovanni demorava cerca de 10 minutos para criar uma boa grelha para o layout de um mapa e, depois, mais 20 minutos para replicá-la umas quantas vezes com pequenas variações para diferentes escalas. Se tivesse de fazer esta operação uma ou duas vezes por semana, no final do ano, teria perdido até 34 horas do seu precioso e muito limitado tempo.

Assim, decidiu contactar um programador *core* do QGIS e pagou cerca de 600€ por uma nova funcionalidade. Um botão para duplicar a grelha selecionada e assim facilitar a reprodução de grelhas existentes. A funcionalidade foi implementada e ficou disponível na próxima versão regular do QGIS (3.40.0).

![texto alternativo](/images/2024/12/duplicate_layout_grid.png)

A um valor de 25€ por hora (apenas um exemplo), as 34 horas representariam aproximadamente 866€. Assim, em menos de 1 ano, o investimento inicial do Giovanni foi totalmente compensado por todo o tempo economizado pela nova funcionalidade.

Se ele tivesse uma empresa com dez trabalhadores a realizar a mesma operação, teria retorno sobre o investimento em menos de um mês!! Se tivesse 100 trabalhadores... bem... acho que já perceberam a ideia. Quanto mais se utiliza a funcionalidade, mais rápido ela fica paga.

Mas este conto ainda não acabou... Estamos a falar de software Open Source. Portanto, esta nova ferramenta, que custou a "alguém" 600 Euros, estava agora disponível para TODOS os utilizadores do QGIS. Gratuitamente!! Sem restrições, sem segregação de licenças.

Agora, imagine que [o QGIS é utilizado diariamente por mais de 500.000 pessoas](https://analytics.qgis.org/) (uma estimativa conservadora, na minha opinião) e que digamos, 0,1% dos utilizadores poupem 20 minutos diários por causa desta nova ferramenta, isso são:

**50.000 pessoas x 20 min x 22 dias úteis = 16.000 horas por Mês!!**

Assim, mesmo com uma taxa muito baixa de 1 Euro por hora, os 600€ podem agora valer 16.000 Euros todos os meses!! (Obviamente, as taxas horárias variam muito dependendo dos salários de cada país. Nos EUA, por exemplo, o [salário de um Analista GIS varia entre cerca de 19 e 35 Euros por hora](https://www.payscale.com/research/US/Skill=Geographic_Information_Systems_(GIS)/Hourly_Rate).)

**A moral deste conto?**

1. Investir tempo e/ou dinheiro no desenvolvimento de projetos Open Source pode ter retornos quase imediatos.
2. O impacto do investimento vai muito além do investidor original, alcançando milhares de utilizadores em todo o mundo que, por algum motivo, não podem fazer o mesmo tipo de investimento ou simplesmente decidiram investir tempo ou dinheiro noutras melhorias do QGIS ou noutro software Open Source que utilizam.

Se tem uma ideia para uma funcionalidade no QGIS ou para corrigir um erro que tornaria a sua vida ou a dos seus colaboradores mais fácil, consulte a lista de [empresas de suporte que são contribuidores *core*](https://www.qgis.org/resources/support/commercial-support/#core-contributors) que podem ajudá-lo a implementá-lo.

**Finalmente, gostaria de agradecer pessoalmente a todos os Giovannis por aí que investem regularmente o seu tempo e/ou dinheiro para melhorar o software Open Source que TODOS podem usar livremente no seu dia a dia.**
