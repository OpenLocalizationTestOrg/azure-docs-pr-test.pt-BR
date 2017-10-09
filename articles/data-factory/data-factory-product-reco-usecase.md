---
title: "aaaData caso de uso de fábrica - as recomendações do produto"
description: "Saiba mais sobre um caso de uso implementado usando o Azure Data Factory junto com outros serviços."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>Caso de uso - recomendações de produtos
A fábrica de dados do Azure é um dos Olá de tooimplement muitos serviços usados Cortana pacote de inteligência de aceleradores de solução.  Consulte a página [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) para obter detalhes sobre este pacote. Neste documento, descrevemos um caso de uso comum que usuários do Azure já resolveram e implementaram usando o Azure Data Factory e outros serviços de componente do Cortana Intelligence.

## <a name="scenario"></a>Cenário
Lojas online normalmente desejam tooentice seus produtos de toopurchase clientes apresentando-los com os produtos que eles são provavelmente toobe interessado em e, portanto, provavelmente toobuy. tooaccomplish, lojas online precisam toocustomize experiência online do seu usuário usando as recomendações de produto personalizadas para esse usuário específico. Essas recomendações personalizadas são toobe feita com base em seus dados atuais e históricos compras comportamento, informações de produto, introduzido recentemente marcas e dados de segmentação de produto e cliente.  Além disso, podem fornecer recomendações de produto de usuário Olá com base na análise de comportamento de uso geral de todos os seus usuários combinados.

objetivo Olá esses revendedores é toooptimize para conversões de clique para venda do usuário e obter maior receita de vendas.  Eles alcançam essa conversão fornecendo recomendações de produtos contextuais, baseadas em comportamento, nas ações e nos interesses do cliente. Para esse caso, usamos lojas online como um exemplo de empresas que desejam toooptimize para seus clientes. No entanto, esses princípios aplicam tooany de negócio que deseja tooengage seus clientes em torno de seus produtos e serviços e aprimorar a experiência de compra dos clientes com recomendações de produtos personalizados.

## <a name="challenges"></a>Desafios
Há muitos desafios enfrentados lojas online durante a tentativa de tooimplement esse tipo de caso de uso. 

Primeiro, dados de tamanhos diferentes e formas devem ser incluídos de várias fontes de dados, locais e na nuvem hello. Esses dados incluem dados de produto, dados de comportamento do cliente históricos e dados de usuário como usuário Olá procura o site de varejo online hello. 

Segundo, recomendações de produtos personalizadas devem ser calculadas e previstas de modo razoável e preciso. Além disso lojas online tooproduct, marca e dados de comportamento e o navegador do cliente, também precisará tooinclude comentários do cliente no passado toofactor compras determinar Olá Olá produto recomendadas para usuário hello. 

Em terceiro lugar, recomendações Olá devem ser imediatamente do produto toohello usuário tooprovide navegação direta e experiência de compra e recomendações hello mais recente e relevante. 

Por fim, revendedores necessário a eficácia de sua abordagem Olá toomeasure rastreando vendas geral êxitos vendas Clique para conversão de venda cruzadam e ajustar recomendações futuras tootheir.

## <a name="solution-overview"></a>Visão geral da solução
Esse exemplo de caso de uso foi resolvido e implementado por usuários reais do Azure pelo uso do Azure Data Factory e outros serviços de componente de Cortana Intelligence, inclusive [HDInsight](https://azure.microsoft.com/services/hdinsight/) e [Power BI](https://powerbi.microsoft.com/).

loja online Olá usa um armazenamento de BLOBs do Azure, um SQL server no local, o banco de dados do Azure SQL e um armazém de dados relacionais como suas opções de armazenamento de dados em todo o fluxo de trabalho de saudação.  armazenamento de blob Olá contém as informações do cliente, os dados de comportamento do cliente e dados de informações do produto. informações de produto Olá dados incluem informações de marca de produto e um catálogo de produtos armazenados no local em um data warehouse do SQL. 

Todos os dados de saudação é combinado e alimentado no produto recomendação sistema toodeliver personalizado recomendações com base em interesses do cliente e as ações, enquanto o usuário Olá procura produtos Olá catálogo no site de saudação. os clientes de saudação também veem produtos que estão relacionados a produto toohello estiverem visualizando com base em padrões de uso de site geral que não estão relacionada tooany um usuário.

![diagrama de casos de uso](./media/data-factory-product-reco-usecase/diagram-1.png)

Gigabytes web bruto de arquivos de log são gerados diariamente no site da loja online hello como arquivos semi-estruturados. Olá arquivos de log da web bruto e informações de catálogo de cliente e produto Olá são incluídas regularmente em um armazenamento de BLOBs do Azure usando a movimentação de dados implantados globalmente da fábrica de dados como um serviço. arquivos de log processados Olá para dia Olá são particionados (por ano e mês) no armazenamento de blob para armazenamento de longo prazo.  [HDInsight do Azure](https://azure.microsoft.com/services/hdinsight/) são arquivos de log bruto de saudação de toopartition usado no blob Olá loja e processe logs de saudação incluída em escala usando scripts de Hive e Pig. Olá blogs particionadas são de dados e processados tooextract Olá necessário entradas para uma recomendação sistema toogenerate Olá personalizado produto recomendações de aprendizado de máquina.

Olá, sistema de recomendação usados para aprendizado de máquina Olá neste exemplo é uma plataforma de recomendação de aprendizado de máquina de código-fonte aberto [Mahout Apache](http://mahout.apache.org/).  Qualquer [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) ou modelo personalizado pode ser aplicado toohello cenário.  modelo de Mahout de saudação é usado toopredict Olá similaridade entre itens no site de saudação com base nos padrões de uso geral e recomendações de saudação personalizada toogenerate com base no usuário individual hello.

Por fim, o conjunto de resultados de saudação de recomendações personalizadas de produto é movido tooa relacional data mart para consumo pelo site do fornecedor de saudação.  conjunto de resultados de saudação também pode ser acessado diretamente do armazenamento de blob por outro aplicativo ou movido tooadditional repositórios para outros consumidores e casos de uso.

## <a name="benefits"></a>Benefícios
Ao otimizar sua estratégia de recomendação de produtos e o alinhamento com as metas de negócios, solução de saudação atendidos da loja online Olá merchandising e objetivos de marketing. Além disso, eles foram toooperationalize capaz e gerenciem o fluxo de trabalho de recomendação de produtos Olá de maneira eficiente, confiável e econômica. abordagem Olá facilitou para eles tooupdate seu modelo e ajustar sua eficácia com base em Olá medidas de vendas sucessos de conversão de clique. Usando o Azure Data Factory, foram capaz de tooabandon o gerenciamento de recursos de nuvem manual caro e demorado e mover o gerenciamento de recursos de nuvem tooon demanda. Portanto, eles foram toosave capaz de tempo e dinheiro e reduzem seu tempo de implantação de toosolution. Exibições de linhagem de dados e a integridade do serviço operacional se tornou fácil toovisualize e solucionar problemas com hello intuitiva Data Factory monitoramento e gerenciamento da interface do usuário disponível no portal do Azure de saudação. A solução agora pode ser agendada e gerenciada de forma que dados concluído confiável produzidos e entregues toousers e dependências de processamento e os dados são gerenciadas automaticamente sem intervenção humana.

Ao fornecer essa experiência de compra personalizada, hello loja online criada um cliente mais competitivo, envolvente experiência e, portanto, aumentar a satisfação do cliente de vendas e geral.

