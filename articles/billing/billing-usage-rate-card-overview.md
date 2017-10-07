---
title: "APIs de cobrança de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre o uso de cobrança do Azure e APIs RateCard, que são insights tooprovide usados para consumo de recursos do Azure e tendências."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Use APIs de cobrança do Azure tooprogrammatically obter informações sobre o uso do Azure
Use dados de uso e recursos de toopull de APIs de cobrança do Azure em suas ferramentas de análise de dados preferencial. Olá uso de recursos do Azure e APIs RateCard podem ajudá-lo a prever com precisão e gerenciar os custos. Olá APIs são implementadas como um provedor de recursos e a parte da família de saudação de APIs expostas pelo hello Azure Resource Manager.  

## <a name="azure-invoice-download-api-preview"></a>API de Download de fatura do Azure (Visualização)
Uma vez Olá [aceitar tiver sido concluída](billing-manage-access.md#opt-in), faturas de download usando a versão de visualização de saudação do [fatura API](/rest/api/billing). Olá recursos incluem:

* **Controle de acesso baseado em função do Azure** -configurar o acesso de políticas em Olá [portal do Azure](https://portal.azure.com) ou por meio [cmdlets do PowerShell do Azure](/powershell/azure/overview) toospecify quais usuários ou aplicativos pode obter acesso dados de uso da assinatura toohello. Os chamadores devem usar tokens padrão do Azure Active Directory para autenticação. Adicione Olá chamador tooeither Olá leitor de cobrança, leitor, proprietário ou colaborador função tooget acesso toohello dados de uso de uma assinatura do Azure específica.
* **Filtragem de data** -Olá Use `$filter` tooget parâmetro data de término do período de todas as faturas de saudação em ordem cronológica inversa por Olá fatura. 

> [!NOTE]
> Esse recurso na primeira versão de visualização e assunto toobackward incompatível alterações pode ser feitas. Atualmente, ele não está disponível para determinadas ofertas de assinatura (não há suporte para EA, CSP, AIO) e para o Azure na Alemanha.

## <a name="azure-resource-usage-api-preview"></a>API de uso de recursos do Azure (visualização)
Saudação de uso do Azure [API de uso do recurso](https://msdn.microsoft.com/library/azure/mt219003) tooget seus dados de consumo do Azure previsto. Olá API inclui:

* **Controle de acesso baseado em função do Azure** -configurar o acesso de políticas em Olá [portal do Azure](https://portal.azure.com) ou por meio [cmdlets do PowerShell do Azure](/powershell/azure/overview) toospecify quais usuários ou aplicativos pode obter acesso dados de uso da assinatura toohello. Os chamadores devem usar tokens padrão do Azure Active Directory para autenticação. Adicione Olá chamador tooeither Olá leitor de cobrança, leitor, proprietário ou colaborador função tooget acesso toohello dados de uso de uma assinatura do Azure específica.
* **Agregações diárias ou por hora** - os chamadores podem especificar se eles desejam seus dados de uso do Azure em buckets por hora ou buckets diários. saudação padrão é diário.
* **Metadados de instância (inclui as marcas de recurso)** – obter os detalhes de nível de instância como Olá uri de recurso totalmente qualificado (/subscriptions/ {id da assinatura} /...), Olá informações do grupo de recursos e as marcas de recurso. Esses metadados ajudam determinística e alocar programaticamente o uso por marcas hello, para casos de uso como a carga entre.
* **Metadados do recurso** -detalhes de recursos, como o nome de medidor hello, medidor categoria, subcategoria do medidor, unidade e região fornecem chamador Olá uma melhor compreensão sobre o que foi consumido. Também estamos trabalhando terminologia de metadados do recurso tooalign em Olá portal do Azure, uso do Azure CSV, EA CSV, de cobrança e outras experiências voltado ao público, toolet correlacionar dados em experiências.
* **Uso para todos os tipos de oferta** – os dados de uso estão disponíveis para todos os tipos de oferta, assim como pré-pago, MSDN, investimento e crédito monetário e EA.

## <a name="azure-resource-ratecard-api-preview"></a>API RateCard de Recursos do Azure (visualização)
Saudação de uso [API do Azure recursos RateCard](https://msdn.microsoft.com/library/azure/mt219005) tooget Olá lista disponíveis do Azure recursos e informações de preço estimadas para cada. Olá API inclui:

* **Controle de acesso baseado em função do Azure** -configurar as políticas de acesso em Olá [portal do Azure](https://portal.azure.com) ou [cmdlets do PowerShell do Azure](/powershell/azure/overview) toospecify quais usuários ou aplicativos pode obter acesso toohello RateCard dados. Os chamadores devem usar tokens padrão do Azure Active Directory para autenticação. Adicione Olá chamador tooeither Olá leitor, proprietário ou colaborador função tooget acesso toohello dados de uso para uma determinada assinatura do Azure.
* **Suporte para pré-pago, MSDN, ofertas de investimento e crédito monetário (EA não tem suporte)** – Esta API fornece informações de taxa no nível da oferta do Azure.  o chamador Olá desta API deve passar em taxas e detalhes do recurso Olá oferta informações tooget. Estamos taxas EA tooprovide atualmente não é possível porque o EA oferece personalizou taxas por registro. 

## <a name="scenarios"></a>Cenários
Aqui estão alguns dos cenários de saudação possibilitado com combinação Olá Olá uso e hello RateCard APIs:

* **Gastos do Azure durante o mês de saudação** -combinação de saudação do uso de Olá RateCard APIs e uso tooget melhor compreensão sobre sua nuvem gastar durante o mês de saudação. Você pode analisar Olá por hora e estimativas de buckets diárias de uso e cobrança.
* **Configurar alertas** – Use Olá uso e hello tooget RateCard APIs estimada consumo de nuvem e encargos e configurar alertas com base em recursos ou monetários com base em.
* **Prever fatura** – obter seu consumo previsto e a nuvem gastam e aplicam toopredict de algoritmos de aprendizado que fatura Olá seria final Olá Olá ciclo de cobrança de máquina.
* **Análise de custo de pré-consumo de** – Use Olá RateCard API toopredict quanto sua fatura seria para seu uso esperado quando você move o tooAzure de cargas de trabalho. Se você tiver cargas de trabalho existentes em outras nuvens ou nuvens privadas, você também pode mapear seu uso com hello Azure taxas tooget gastam uma estimativa melhor do Azure. Isso proporciona estimativa Olá capacidade toopivot na oferta e comparar e contrastar entre tipos de oferta diferente Olá além pré-pago, como o investimento e crédito monetário. Olá API também lhe Olá capacidade toosee custo as diferenças por região e permite que você toodo um toohelp de análise de custo e se você tomar decisões de implantação.
* **Hipóteses** -
  
  * Você pode determinar se ele é mais econômico toorun cargas de trabalho em outra região, ou em outra configuração de saudação recursos do Azure. Recursos do Azure, os custos podem ser diferentes com base em Olá região do Azure que você está usando.
  * Você também pode determinar se outro tipo de oferta do Azure oferece uma melhor taxa em um recurso do Azure.
  
## <a name="partner-solutions"></a>Soluções de parceiros
[O uso do Microsoft Azure e RateCard APIs habilitar Cloudyn tooProvide ITFM para clientes](billing-usage-rate-card-partner-solution-cloudyn.md) descreve a experiência de integração Olá oferecida pelo parceiro de API de cobrança do Azure [Cloudyn](https://www.cloudyn.com/microsoft-azure/). Este artigo fala sobre suas experiências e inclui um vídeo que mostra como você pode usar Cloudyn e Olá insights de tooget de APIs de cobrança do Azure dos dados de consumo do Azure.

[A integração de API de cobrança do Microsoft Azure e de cruiser em nuvem](billing-usage-rate-card-partner-solution-cloudcruiser.md) descreve como [Express do cruiser em nuvem para Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) funciona diretamente do portal do Windows Azure Pack (WAP) hello. Sem problemas, você pode gerenciar ambos os aspectos operacionais e financeiros de saudação da saudação Microsoft Azure privado ou hospedado em nuvem pública de uma interface de usuário único.   

## <a name="next-steps"></a>Próximas etapas
* Consulte exemplos de código Olá no GitHub:
  * [Exemplo de código da API de Fatura](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Exemplo de código da API de Uso](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Exemplo de código da API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn mais sobre hello Azure Resource Manager, consulte [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md). 

* Para obter mais informações no pacote de saudação de ferramentas de gastar toohelp necessário obter uma compreensão da nuvem, consulte artigo de Gartner Olá [guia de mercado para as ferramentas de gerenciamento de TI financeiro (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

