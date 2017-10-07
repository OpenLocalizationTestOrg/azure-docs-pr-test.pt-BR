---
title: "aaaFAQ para bancos de dados ClearDB MySql com o serviço de aplicativo do Azure | Microsoft Docs"
description: "Respostas a perguntas toocommon sobre o uso de bancos de dados MySQL de ClearDB com o serviço de aplicativo do Azure."
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>Perguntas frequentes sobre bancos de dados MySql do ClearDB com o Serviço de Aplicativo do Azure
Estas perguntas frequentes respondem a dúvidas comuns sobre como usar e adquirir os bancos de dados MySQL do ClearDB para aplicativos Web do Azure.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Quais são as minhas opções para o MySQL no Azure?
Você tem várias opções:

* [Banco de dados MySQL compartilhado do ClearDB](/marketplace/partners/cleardb/databases/)
* [Clusters MySQL Premium do ClearDB](/marketplace/partners/cleardb-clusters/cluster/)
* [Cluster MySQL em execução em uma VM do Azure](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Instância única do MySQL em execução em uma VM do Azure](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB é um serviço de hospedagem MySQL e gerencia a infraestrutura do MySQL Olá para você. Quando você executa seu próprio cluster MySQL ou banco de dados em uma máquina Virtual do Azure, você tem tooset servidor MySQL de saudação e mantê-lo atualizado com os patches.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>É necessário um cartão de crédito para aplicativo da Web de saudação + modelo MySQL no Azure Marketplace de Olá?
Isso depende de tipo de saudação de assinatura que você está usando. Veja a seguir alguns tipos de assinatura normalmente usadas:

* [Pré-pago](/offers/ms-azr-0003p/): exige um cartão de crédito, e quando você comprar um banco de dados MySQL pago, ele será cobrado no cartão de crédito.
* [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/): inclui créditos para uso com os serviços do Microsoft Azure, mas não permite a compra de recursos de terceiros. assinatura habilitada do serviços de terceiros toopurchase ou um banco de dados MySQL pago necessário toouse um cartão de crédito. Para aplicativos Web, você pode criar um banco de dados MySQL do ClearDB GRATUITO.
* [Assinatura do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) e **desenvolvimento teste MSDN pré-pago**: tooFree semelhante avaliação, uma assinatura do MSDN requer toohave toopurchase um cartão de crédito uma solução paga do MySQL de ClearDB.
* [EA (Enterprise Agreement)](https://azure.microsoft.com/pricing/enterprise-agreement/): os clientes de EA recebem em uma fatura consolidada e separada uma cobrança por seu EA a cada trimestre referente a todas as suas compras (de terceiros) no Azure Marketplace. Você será cobrado fora Olá investimento para todas as compras do marketplace. Observe que, neste momento, o armazenamento do Azure não está disponível toocustomers registrados no Azerbaijão, Croácia, Noruega e Porto Rico. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): você só pode criar bancos de dados ClearDB GRATUITOS para Aplicativos Web. Não há nenhum limite no número de saudação do MySQL de ClearDB livre de bancos de dados que você pode criar. Observe que bancos de dados gratuitos não são toobe usado para aplicativos da web de produção, como esse serviço é destinado apenas para avaliação.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>Por que eu fui cobrado US $3.50 para um aplicativo Web + MySQL do hello Azure Marketplace?
opção de banco de dados padrão de saudação é Titan, que é de US $3.50. Nós não mostrar o custo de saudação durante a criação do banco de dados e, por engano, você pode adquirir um banco de dados que você não pretendia. Podemos tentar toofind uma experiência de saudação do modo tooimprove mas até lá, você deve verificar todas as suas camadas de preços selecionadas para o aplicativo web e o banco de dados antes de clicar em **criar** e iniciar a implantação de saudação de recursos de saudação.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>Estou executando o MySQL em minha própria máquina virtual do Azure. Posso conectar meu banco de dados de toomy de aplicativo web do Azure?
Sim. Você pode conectar o banco de dados de tooyour de aplicativo da web como sua VM do Azure concedeu acesso remoto tooyour web app. Para obter mais informações, confira [Instalar o MySQL em uma máquina virtual](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>Em quais países os clusters MySQL do ClearDB Premium têm suporte?
[Clusters de ClearDB Premium MySQL](/marketplace/partners/cleardb-clusters/cluster/) estão disponíveis em todas as regiões do Azure no mundo todo, com exceção de saudação do Austrália, Índia, Sul do Brasil e na China.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>É possível criar um novo toocreating anteriores de cluster um banco de dados com a solução de cluster ClearDB premium?
Não, não há suporte para a criação de clusters ClearDB vazios. Olá portal do Azure permite que você toocreate bancos de dados em um cluster, o que pode criar um novo cluster no hello simultaneamente.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>Será eu avisado se eu tentar toodelete um banco de dados ClearDB MySQL está em uso por um de meus aplicativos?
Não, o Azure não avisará se você excluir uma compra feita no Marketplace da qual seu aplicativo dependa.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>Em quais regiões eu posso criar os bancos de dados ClearDB?
Marketplace do Azure não está disponível toocustomers registrados no Azerbaijão, Croácia, Noruega ou Porto Rico. O ClearDB não está disponível nessas regiões.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>Qual tipo de preço eu devo escolher para um aplicativo Web de produção e banco de dados?
Use Basic ou um tipo de preço mais alto para aplicativos Web. Para o ClearDB, recomendamos um plano Saturn ou Jupiter. Analisar recursos hello e limitações de cada camada de preços para ambos [aplicativos Web](https://azure.microsoft.com/pricing/details/app-service/) e [bancos de dados MySQL de ClearDB](/marketplace/partners/cleardb/databases/) Olá toochoose que atenda às suas necessidades.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>Como atualizar meu banco de dados ClearDB de tooanother de um plano?
Em Olá [portal do Azure](https://portal.azure.com), você pode expandir um ClearDB hospedagem banco de dados compartilhado. Leia este [artigo](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn mais. Atualmente não há suporte para atualização para ClearDB Premium clusters em Olá portal do Azure.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Por que não consigo ver meu banco de dados ClearDB no portal do Azure?
Se nós criamos o banco de dados ClearDB usando o Gerenciador de recursos do Azure ou [novo Portal do Azure](https://portal.azure.com), não estarão visível no hello [antigo Portal do Azure](https://manage.windowsazure.com). toowork-esse problema é toolink seu banco de dados manualmente toohello web app. Da mesma forma se criar banco de dados ClearDB Olá [portal antigo](https://manage.windowsazure.com) você não poderá ser capaz de toosee seu banco de dados em Olá [novo Portal do Azure](https://portal.azure.com). Não há nenhuma solução alternativa para o cenário último hello.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>Quem devo contatar para obter suporte quando meu banco de dados ficar inativo?
Entre em contato com o [Suporte do ClearDB](https://www.cleardb.com/developers/help/support) para quaisquer problemas relacionados ao banco de dados. Prepare-se tooprovide com as suas informações de assinatura do Azure.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>Posso criar usuários adicionais para minha solução de cluster de banco de dados MySQL ClearDB?
Não. Não é possível criar usuários adicionais, mas você pode criar bancos de dados adicionais no cluster do banco de dados ClearDB.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Bancos de dados de série Basic/Pro podem ser atualizados no local semelhante tooPlanetary planos atualmente no portal de ClearDB?
Sim, a série de bancos de dados Basic pode ser atualizada no local (Basic 60 à Basic 500). A série Pro pode ser atualizada in-loco (Pro 125 à Pro 1000), com exceção da Pro 60. Não damos suporte para atualizar o banco de dados Pro 60 atualmente. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>Ao migrar meus recursos de um tooanother de assinatura, meu banco de dados ClearDB MySQL obter migrado também?
Quando você executar recursos de migração entre assinaturas, serão aplicadas algumas [limitações](app-service-web/app-service-move-resources.md) . O banco de dados MySQL ClearDB é um serviço de terceiros e, portanto, não será migrado durante a migração da assinatura do Azure. Se você não gerenciar a migração de saudação do seu MySQL toomigrating anterior do Azure do banco de dados recursos, o ClearDB MySQL bancos de dados podem ser desabilitados. Primeiro, migre manualmente os bancos de dados e, em seguida, realize a migração da assinatura do Azure para seu aplicativo Web. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>Acerto Olá limite de gastos na minha assinatura. Eu removi limite hello e meu serviço de aplicativo está online, mas o banco de dados de saudação não está acessível. Como habilitar novamente o banco de dados de ClearDB Olá?
Entre em contato com [ClearDB suporte](https://www.cleardb.com/developers/help/support) toore-habilitar banco de dados de saudação. Forneça suas informações de assinatura do Azure e nome do banco de dados.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>Pode transferir um banco de dados ClearDB de uma assinatura do cartão de crédito assinatura tooan EA?
Bancos de dados existentes ClearDB usam cartão de crédito de saudação associada a assinaturas existentes hello. toouse uma assinatura de EA precisar toomigrate dados tooa novo banco de dados:

* Compre um novo banco de dados ClearDB com sua assinatura do EA.
* Migre dados tooyour novo banco de dados.
* Atualize seu aplicativo toouse Olá novo banco de dados.
* Exclua o banco de dados ClearDB antigo.

Quando você cria um novo aplicativo web com o MySQL (ClearDB) ou cria um banco de dados MySQL (ClearDB), Olá assinatura que você escolhe determina como você pagará serviço hello. Com uma assinatura de EA, bloquearemos não compras Olá dos serviços de terceiros hello como ClearDB no hello portal do Azure. As assinaturas de EA são cobradas fora do Compromisso Monetário e são cobradas trimestralmente e mediante inadimplência. cliente EA Olá teria tooset um método de pagamento, como um cartão de crédito toopay para quaisquer serviços do marketplace de terceiros.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>Onde posso ver encargos Olá para recursos de ClearDB em uma assinatura de EA?
Para clientes de EA direto, encargos do Marketplace do Azure estão visíveis na Olá Portal Empresarial. Observe que todas as compras e consumo no marketplace são faturadas fora do Compromisso monetário e são cobradas trimestralmente e mediante inadimplência. Clientes EA têm toopay diretamente de provedores de serviços de terceiros de toohello e pode portanto, permitindo que um método de pagamento, como um cartão de crédito com seu EA conta.

Clientes EA indiretos podem encontrar suas assinaturas do Azure Marketplace em Olá **gerenciar assinaturas** página Olá Enterprise Portal, mas preços está oculto. Os clientes devem entrar em contato com seus LSPs para saber mais sobre encargos do Marketplace.

Acesso tooAzure Marketplace para serviços de terceiros pode ser gerenciado por seus administradores de registro do Azure EA. Eles podem desabilitar ou habilitar novamente o acesso too3rd parte compras de saudação repositório em gerenciar contas e assinaturas na seção contas Olá Olá Portal Empresarial.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>Quem devo contatar para perguntas sobre minha fatura para serviços do ClearDB em minha assinatura do EA?
Entre em contato com [atendimento Enterprise](http://aka.ms/AzureEntSupport) com toobilling quanto em seu registro de EA. Olá, equipe de suporte do Portal EA responderão sua pergunta ou ajudar a resolver o problema.

## <a name="more-information"></a>Mais informações
[Perguntas frequentes sobre o Azure Marketplace](/marketplace/faq/)

