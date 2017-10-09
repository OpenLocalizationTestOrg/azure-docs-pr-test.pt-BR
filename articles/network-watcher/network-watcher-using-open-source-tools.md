---
title: "padrões de tráfego de rede aaaVisualize com ferramentas de software livre e o observador de rede do Azure | Microsoft Docs"
description: "Esta página descreve como de captura de pacote de rede Inspetor toouse com tooand de padrões de tráfego Capanalysis toovisualize de suas VMs."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Visualizar tooand de padrões de tráfego de rede de suas VMs usando ferramentas de software livre

Captura de pacote contém dados de rede que permitem a análise forense tooperform e inspeções profundas de pacote. Há abre muitas ferramentas de origem, você pode usar tooanalyze pacote capturas toogain informações sobre a sua rede. Uma dessas ferramentas é a CapAnalysis, uma ferramenta de visualização de captura de pacote de software livre. Visualização de dados de captura de pacote é uma maneira importante que tooquickly derivar ideias sobre padrões e as anomalias dentro de sua rede. As visualizações também fornecem um meio de compartilhar essas informações de maneira facilmente consumível.

Observador de rede do Azure fornece que Olá capacidade toocapture captura dados valiosos, permitindo que o pacote de tooperform em sua rede. Neste artigo, fornecemos um passo a passo de como toovisualize e obtenha informações do pacote de captura usando CapAnalysis com o observador de rede.

## <a name="scenario"></a>Cenário

Você tem um aplicativo da web simples implantado em uma máquina virtual no Azure deseja toouse código-fonte aberto ferramentas toovisualize seu tooquickly de tráfego de rede identificar padrões de fluxo e todas as anomalias possíveis. Com o observador de rede, você poderá obter uma captura de pacote de seu ambiente de rede e armazená-lo diretamente em sua conta de armazenamento. CapAnalysis, captura de pacote do hello diretamente saudação do blob de armazenamento de ingestão e visualizar o seu conteúdo.

![cenário][1]

## <a name="steps"></a>Etapas

### <a name="install-capanalysis"></a>Instale o CapAnalysis

tooinstall CapAnalysis em uma máquina virtual, você pode consultar instruções oficial toohello https://www.capanalysis.net/ca/how-to-install-capanalysis aqui.
Acessar CapAnalysis remotamente, precisamos tooopen porta 9877 na sua VM, adicionando uma nova regra de segurança de entrada. Para obter mais informações sobre como criar regras em grupos de segurança de rede, consulte muito[criar regras em um NSG existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Depois que a regra de saudação foi adicionada com êxito, você deve ser capaz de tooaccess CapAnalysis de`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Use o observador de rede do Azure toostart sessão de captura de um pacote

Observador de rede permite tráfego de tootrack toocapture pacotes dentro e fora de uma máquina virtual. Você pode consultar as instruções de toohello em [captura de pacote de gerenciamento com o observador de rede](network-watcher-packet-capture-manage-portal.md) toostart uma sessão de captura de pacote. Esta captura de pacote pode ser armazenada em um toobe de blob de armazenamento acessado por CapAnalysis.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Carregar um tooCapAnalysis de captura de pacote
Diretamente, você pode carregar uma captura de pacote utilizada pelo observador de rede usando o guia de "Da URL de importação" hello e fornecendo um blob de armazenamento do link toohello onde a captura de pacote de saudação é armazenada.

Ao fornecer um link tooCapAnalysis, verifique se tooappend uma URL de blob de armazenamento de toohello token SAS.  toodo isso, navegue tooShared assinatura de acesso da conta de armazenamento hello, designar Olá permissões concedida e pressione Olá gerar SAS botão toocreate um token. Em seguida, você pode acrescentar essa URL de blob de armazenamento SAS token toohello pacote captura.

Olá URL resultante será parecida com isto: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Análise de capturas de pacote

CapAnalysis oferece várias toovisualize de opções sua captura de pacote, cada fornecendo análise de uma perspectiva diferente. Com esses resumos visuais, você pode entender as tendências do tráfego de rede e identificar rapidamente qualquer atividade incomum. Alguns desses recursos são mostrados na Olá lista a seguir:

1. Tabelas de fluxo

    Fornece essa tabela Olá lista de fluxos de dados do pacote de saudação, Olá associado Olá fluxos de carimbo de hora e Olá vários protocolos associados fluxo hello, assim como o IP de origem e de destino.

    ![página de fluxo do capanalysis][5]

1. Visão geral do protocolo

    Este painel permite que você tooquickly ver distribuição de saudação do tráfego de rede ao longo do hello diversos protocolos e regiões geográficas.

    ![visão geral do protocolo do capanalysis][6]

1. Estatísticas

    Este painel permite que você tooview estatísticas de tráfego de rede – bytes enviados e recebidos da origem e destino IPs, fluxos para cada fonte hello e destino IPs, o protocolo usado para vários fluxos e a duração de saudação de fluxos.

    ![estatísticas do capanalysis][7]

1. Geomap

    Este painel fornece uma exibição de mapa de seu tráfego de rede com cores dimensionamento toohello volume de tráfego de cada país. Você pode selecionar países realçados tooview fluxo adicional estatísticas, como a proporção de saudação de dados enviados e recebidos de IPs esse país.

    ![geomap][8]

1. Filtros

    O CapAnalysis fornece um conjunto de filtros para análise rápida dos pacotes específicos. Por exemplo, você pode escolher dados de saudação toofilter por informações específicas do protocolo toogain nesse subconjunto de tráfego.

    ![filtros][11]

    Visite [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn mais sobre os recursos dos todos os CapAnalysis.

## <a name="conclusion"></a>Conclusão

O recurso de captura de pacote do observador de rede permite que você toocapture Olá dados tooperform necessário análise forense e entender melhor o tráfego de rede. Nesse cenário, mostramos como as capturas de pacote do observador de rede podem ser facilmente integradas a ferramentas de visualização de software livre. Usando ferramentas de software livre, como captura CapAnalysis toovisualize pacotes, você pode executar a inspeção profunda de pacotes e identificar rapidamente as tendências em seu tráfego de rede.

## <a name="next-steps"></a>Próximas etapas

toolearn mais informações sobre logs de fluxo do NSG, visite [NSG fluxo logs](network-watcher-nsg-flow-logging-overview.md)

Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
