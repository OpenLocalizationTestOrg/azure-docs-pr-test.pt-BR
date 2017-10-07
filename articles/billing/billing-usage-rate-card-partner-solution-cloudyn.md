---
title: o uso do Azure e RateCard APIs habilitar Cloudyn de aaaMicrosoft tooProvide ITFM para clientes | Microsoft Docs
description: "Fornece uma perspectiva exclusiva do parceiro de cobrança do Microsoft Azure Cloudyn, em suas experiências integrar Olá APIs de cobrança do Azure em seus produtos.  Isso é especialmente útil para clientes do Azure e Cloudyn que estejam interessados em usar/experimentar o Cloudyn para serviços do Azure."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>O uso do Microsoft Azure e RateCard APIs habilitar Cloudyn tooProvide ITFM para clientes
Cloudyn, um parceiro de desenvolvimento da Microsoft e uma fornecedora líder de recursos de gerenciamento de nuvem, foi escolhido para uma visualização privada do hello novas APIs de RateCard e uso de recursos do Microsoft Azure.  Olá API de uso fornece dados do access tooestimated consumo do Azure para uma assinatura. Olá API RateCard fornece informações sobre preços completas de todos os serviços do Azure, para clientes não - Enterprise contrato EA. Quando integradas, essas APIs fornecem uma base de informações completa para inseração em ferramentas gestão financeira de TI (ITFM), como as fornecidas pelo Cloudyn.

## <a name="introduction"></a>Introdução
Olá chamada "multiplicação" de dados de saudação API de uso com dados de saudação RateCard API (preço de uso [unidades] [$unit] = detalhadas de uso e o custo) cria hello mais granular, precisas e confiáveis as informações de cobrança disponíveis para o Azure hoje.

![Visão geral de ITFM][1]

Consumir essas APIs fornece informações importantes sobre o uso de clientes e os custos, permitindo que as contas de clientes tooanalyze Cloudyn em um modo programático simple e tooperform várias tarefas ITFM para seus clientes.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Integração Cloudyn com hello RateCard e APIs de uso
Olá RateCard API exige vários parâmetros de entrada – como informações de região, moeda e localidade – mas hello mais importante de um é OfferDurableID, que especifica o tipo de saudação do cliente de saudação de oferta do Azure está usando (pré-pago, herdado 6 e 12 meses compromisso planos, MSDN oferece, MPN ofertas, ofertas promocionais e outros). Olá OfferDurableID pode ser encontrado na Olá [o uso do Azure e o portal de cobrança](https://account.windowsazure.com/Subscriptions), sob hello "Oferecem ID" hello assinatura determinada.

Após o registro para [Cloudyn para o Azure](https://www.cloudyn.com/microsoft-azure/) services, os clientes podem adicionar seu código OfferDurableID, que permite Cloudyn toopull suas informações de preços relevantes por meio de saudação RateCard API.  Informações sobre diferentes tipos de saudação de ofertas podem ser encontradas uma saudação [detalhes da oferta do Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) página.

![Visão geral do mecanismo de IFTM do Cloudyn][2]

Cloudyn usa que ambos Olá APIs RateCard e o uso em adição toohello API de desempenho do Azure, toocreate de camadas adicionais de visualização, análise, alertas, relatórios, custo recomendações viáveis, fornecendo um confiável a clientes do Azure e gerenciamento ferramenta ITFM de nuvem empresarial.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Casos de uso de IFTM do Cloudyn habilitados pela integração da API de Uso e a RateCard
Casos de uso comuns de IFTM do Cloudyn habilitados pela integração da API de Uso e a RateCard incluem:

* **Análise de custo** -permite que a nuvem custa toobe dividido tooany nativo de identificação de dimensão (provedor de serviço, conta, região etc.). Olá uso do Azure e RateCard APIs tornam esta uma tarefa fácil, fornecendo a divisão mais granular Olá de dados de uso e o custo por conta, que é, em seguida, agrupado e filtrado por Cloudyn e apresentado toohello usuário, em um formato gráfico ou de tabela.

![Gráfico de pizza de análise de custo][3]

* **Custo de alocação 360** -habilita finanças e Olá toouncover de gerenciadores de IT real custam divisão, os drivers e as tendências de sua implantação de nuvem. Mais permite aos gerentes tooeasily despesas de implantação associado com unidades de negócios, departamentos, regiões e muito mais, fornecendo precedentes ideias sobre os custos de nuvem e facilita a empresa estornos e showbacks. Olá uso do Azure e APIs RateCard servem como mecanismo de alocação de custo da entrada tooCloudyn, que complementa Olá APIs definindo métodos e lógica de negócios para alocar recursos marcados ou untaggable.

![Gráfico de alocação de custos 360][4]

* **Dimensionamento econômico** -fornece recomendações de dimensionamento da direita para subutilizados máquinas virtuais, reduzindo, assim, a saudação as despesas em máquinas de provisionamento excessivo ou muito grandes. Ele faz isso examinando a CPU da máquina virtual e métricas de RAM (por meio da API de Desempenho), das horas de tempo de execução (por meio do uso da API) e o custo (por meio da API RateCard). Cloudyn, em seguida, fornece recomendações de dimensionamento à direita com base nos recursos de CPU ou memória RAM subutilizados (desempenho) e calcula economia estimada multiplicando o delta de preço da saudação (RateCard) entre VMs Olá por Olá tempo-utilização real (uso) da saudação máquina subutilizada.

![Custos reduzidos de dimensionamento][5]

* **Recomendações de portabilidade de nuvem** - Fornece consultoria financeira sobre a portabilidade de nuvem. Ele examina custos atuais de um usuário de recursos de nuvem que são implantados em fornecedores de nuvem principal e o compara toohello custo de uma implantação equivalente no Azure. Em seguida, fornece granular, por recurso, financeiramente com base em movimentando tooAzure recomendações. Depois de avaliar uma implantação equivalente Olá necessária no Azure (com base nas preferências de usuário e métricas de desempenho), Cloudyn usa Olá RateCard API tooevaluate Olá custo implantação equivalente Olá no Azure.
* **Relatórios de desempenho** -habilitado pelo API do desempenho do Azure, esses relatórios fornecem uma matriz de recursos da utilização da CPU e RAM toooptimization recomendações. Abaixo está um exemplo de relatório de utilização de instância, apresentando a divisão de instância por utilização média da CPU.

![Relatórios de desempenho][6]

* **Gerente de categoria** -um recurso poderoso do Cloudyn que traz ordem toounorganized recursos de nuvem. Ele fornece a usuários Olá liberdade toocreate suas próprias categorias exclusivas (tags) para medir e relatórios que está de acordo com as práticas comerciais efetivas. Além disso, os usuários podem facilmente regular e categorizar a marcação inconsistente (por exemplo, erros de digitação e outras discrepâncias) e detectar automaticamente os recursos marcados para uma atribuição de custo precisa.

![Gerenciador de categoria][7]

## <a name="video"></a>Vídeo
Aqui está um breve vídeo que mostra como um cliente do Azure pode usar Cloudyn para o Azure e Olá APIs de cobrança do Azure, toogain ideias de seus dados de consumo do Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Iniciar um livre [Cloudyn para o Azure](https://www.cloudyn.com/microsoft-azure/) toosee avaliação como você pode obter custo transparência com relatórios personalizados e análises para sua implantação de nuvem do Microsoft Azure.
* Consulte [obter ideias sobre o consumo de recursos do Microsoft Azure](billing-usage-rate-card-overview.md) para uma visão geral das APIs de RateCard e Olá uso de recursos do Azure.
* Check-out Olá [referência da API REST do Azure cobrança](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) para obter mais informações sobre as duas APIs, que fazem parte do conjunto de saudação de APIs fornecidas pelo hello Azure Resource Manager.
* Se você quiser toodive diretamente no código de exemplo hello, check-out de nosso Microsoft Azure cobrança API exemplos de código em [exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Saiba mais
* toolearn mais sobre as ofertas do Microsoft Azure Enterprise Agreement (EA), visite [licenciamento do Azure para Olá Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) artigo toolearn mais sobre hello Azure Resource Manager.
* Para obter informações adicionais no pacote de saudação de ferramentas de gastar toohelp necessária em uma compreensão da nuvem, consulte muito Gartner artigo [guia de mercado para as ferramentas de gerenciamento de TI financeiro (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
