---
title: aaaUnderstand do Azure detalhadas de uso | Microsoft Docs
description: "Saiba como tooread e entender as seções de saudação do seu uso detalhadas CSV para sua assinatura do Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Compreenda os termos nos encargos de uso detalhado do Microsoft Azure 
Olá detalhadas de uso arquivo CSV de encargos contém diariamente e encargos de uso de nível de medidor para Olá atual período de cobrança. 

tooget seu arquivo de uso detalhadas, consulte [como tooget sua cobrança do Azure fatura e dados de uso diário](billing-download-azure-invoice-daily-usage-date.md).
Ele está disponível em um formato de arquivo .csv (valores separados por vírgulas) que pode ser aberto em um aplicativo de planilhas. Se você vir duas versões disponíveis, baixe a versão 2. Que é o formato de arquivo mais atual da saudação.

Encargos de uso são Olá total **mensal** encargos em uma assinatura. Os encargos de uso não levam em consideração nenhum crédito nem desconto.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>Descrições e termos detalhados do arquivo de uso detalhado
Olá seções a seguir descrevem termos importantes hello, mostrados na versão 2 do arquivo de uso detalhadas hello.

### <a name="statement"></a>Instrução
seção superior Olá Olá detalhadas uso CSV mostra Olá serviços de arquivo que você usou durante o período de cobrança Olá mês. Olá tabela a seguir lista termos hello e descrições mostradas nesta seção.

| Termo | Descrição |
| --- | --- |
|Período de Cobrança |período de cobrança Hello quando metros Olá foram usados |
|Categoria de medidor |Identifica o serviço de nível superior Olá para uso de saudação |
|Subcategoria de medidor |Define o tipo de saudação do serviço do Azure que pode afetar a taxa de saudação |
|Nome do medidor |Identifique Olá unidade de medida para o medidor hello está sendo consumido |
|Região do medidor |Identifica o local de saudação do datacenter Olá para determinados serviços que são cobradas com base na localização do datacenter |
|SKU |Identifica o identificador de sistema exclusivo Olá para cada medidor do Azure |
|Unidade |Identifica Olá serviço Olá cobrado na unidade. Por exemplo, GB, horas, 10.000 s. |
|Quantidade consumida |quantidade de saudação do medidor Olá usado durante o período de cobrança Olá |
|Quantidade incluída |quantidade de saudação do medidor Olá incluído sem nenhum custo em seu período de cobrança atual |
|Quantidade de excesso |Mostra Olá diferença entre Olá quantidade consumida e Olá quantidade incluída. A cobrança é feita com base nessa quantidade. Ofertas de pré-pago com nenhuma quantidade incluídos com a oferta de hello, esse total é Olá mesmo Olá quantidade consumida. |
|Dentro do Compromisso |Mostra os encargos de medidor Olá são subtraídos do valor do seu compromisso associado a sua oferta de 6 ou 12 meses. Os encargos do medidor são subtraídos em ordem cronológica. |
|Moeda |moeda Olá usada no seu período de cobrança atual |
|Excedente |Mostra os encargos de medidor Olá excederam o valor do seu compromisso associado a sua oferta de 6 ou 12 meses |
|Tarifa de Compromisso |Mostra a taxa de confirmação de saudação com base na quantidade de confirmação total Olá associada a sua oferta de 6 ou 12 meses |
|Tarifa |taxa de saudação, que você será cobrado por unidade faturável |
|Valor |Mostra o resultado de saudação da multiplicação Olá coluna quantidade média por coluna de taxa de saudação. Não se Olá que não excede a quantidade consumida hello quantidade incluída, há nenhum encargo nesta coluna. |

### <a name="daily-usage"></a>Uso diário

Olá seção diária de uso do arquivo CSV de saudação mostra detalhes de uso que afetam as taxas de cobrança hello. Olá tabela a seguir lista termos hello e descrições mostradas nesta seção.

| Termo | Descrição |
| --- | --- |
|Data de Uso |Data de saudação quando o medidor Olá foi usado |
|Categoria de medidor |Identifica o serviço de nível superior Olá para o qual este uso pertence |
|ID de medidor |Olá cobrado o identificador de medidor que tenha usado o uso de cobrança tooprice |
|Subcategoria de medidor |Define o tipo de serviço do Azure Olá que pode afetar a taxa de saudação |
|Nome do medidor |Identifique Olá unidade de medida para o medidor hello está sendo consumido |
|Região do medidor |Identifica o local de saudação do datacenter Olá para determinados serviços que são cobradas com base na localização do datacenter |
|Unidade |Identifica unidade Olá esse medidor Olá é cobrado. Por exemplo, GB, horas, 10.000 s. |
|Quantidade consumida |quantidade de saudação do medidor de saudação que foi consumido para esse dia |
|Local do recurso |Identifica Olá datacenter onde medidor hello está sendo executado |
|Serviço consumido |Olá serviços da plataforma Azure que você usou |
|Grupo de recursos |grupo de recursos Olá no qual hello está sendo executado no medidor implantado. <br/><br/>Para saber mais, consulte [Visão geral do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
|ID da instância | Identificador Olá medidor hello. <br/><br/> Identificador de saudação contém nome de saudação que você especificar para o medidor hello quando ele foi criado. É o nome de saudação do recurso de hello ou Olá totalmente qualificado a ID de recurso. Para saber mais, confira [API do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|Marcas | Marca atribuir toohello medidor. Use marcas toogroup registros de cobrança.<br/><br/>Por exemplo, você pode usar marcas toodistribute custos pelo departamento de saudação que usa o medidor hello. Serviços que oferecem suporte a marcas de emissão são máquinas virtuais, armazenamento e serviços de rede provisionados usando Olá [API do Gerenciador de recursos do Azure](https://docs.microsoft.com/rest/api/resources/resources). Para saber mais, confira [Organizar os recursos do Azure com marcas](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/). |
|Informações Adicionais |Metadados específicos ao serviço. Por exemplo, um tipo de imagem para uma máquina virtual. |
|Informações do Serviço 1 |nome de projeto Olá Olá serviço pertence tooon sua assinatura |
|Informações do Serviço 2 |Campo herdado que captura os metadados específicos do serviço opcional |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>Como ter certeza de que encargos Olá no meu arquivo detalhadas de uso estão corretos?
Se há um encargo em seu arquivo de uso detalhado sobre o qual você deseja obter mais detalhes, consulte [Entenda sua fatura do Microsoft Azure.](./billing-understand-your-bill.md)

## <a name="external"></a>E quanto a cobranças de serviço externo?
Serviços externos (também conhecidos como pedidos do Marketplace) são fornecidos por fornecedores de serviços independentes e são cobrados separadamente. encargos de saudação não aparecem nos Olá fatura do Azure. mais, consulte toolearn [entender o Azure cobra serviço externo](billing-understand-your-azure-marketplace-charges.md).

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?) para resolver seu problema rapidamente.
