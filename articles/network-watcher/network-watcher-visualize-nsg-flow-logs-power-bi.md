---
title: "logs de aaaVisualizing fluxo de grupo de segurança de rede do Azure com o Power BI | Microsoft Docs"
description: "Esta página descreve como o fluxo NSG toovisualize registra com o Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Visualização de logs de fluxo do grupo de segurança de rede com o Power BI

Os logs de fluxo de grupo de segurança de rede permitem tooview a informações sobre o tráfego IP de entrada e saída em grupos de segurança de rede. Esses logs de fluxo Mostrar saídas e fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (origem/destino IP, porta de origem/destino, protocolo), e se o tráfego de saudação é permitido ou negado.

Pode ser difícil toogain insights em fluxo de log de dados pesquisando manualmente os arquivos de log de saudação. Neste artigo, fornecemos um toovisualize solução seu fluxo mais recente logs e saiba mais sobre o tráfego na rede.

## <a name="scenario"></a>Cenário

Olá cenário a seguir, conectamos conta de armazenamento do Power BI desktop toohello que configuramos como coletor Olá para nossos dados NSG fluxo de log. Depois de nos conectarmos tooour conta de armazenamento, Power BI baixa e analisa Olá logs tooprovide uma representação visual do tráfego de saudação que é registrado por grupos de segurança de rede.

Usando visuais Olá fornecidos no modelo de saudação, que você pode examinar:

* Os principais locutores
* Dados de fluxo de série temporal por decisão de regra e direção
* Fluxos de endereço MAC da interface de rede
* Fluxos de NSG e regra
* Fluxos de porta de destino

modelo de saudação fornecido é editável para que você pode modificá-lo tooadd novos dados, visuais, ou editar consultas toosuit suas necessidades.

## <a name="setup"></a>Configuração

Antes de começar, você deve habilitar o registro em log de fluxo do grupo de segurança de rede em um ou mais grupos de segurança de rede em sua conta. Para obter instruções sobre como habilitar a segurança de rede de fluxo de logs, consulte toohello artigo a seguir: [registro em log tooflow de Introdução para grupos de segurança de rede](network-watcher-nsg-flow-logging-overview.md).

Você também deve ter o cliente do Power BI Desktop saudação instalado em seu computador e suficiente liberar espaço em sua máquina toodownload e carga Olá dados de log que existe na conta de armazenamento.

![Diagrama do Visio][1]

### <a name="steps"></a>Etapas

1. Baixe e abra Olá seguindo o modelo do Power BI no hello aplicativo de área de trabalho do Power BI [fluxo de rede Inspetor PowerBI logs de modelo](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Digite os parâmetros de consulta Olá necessária
    1. **StorageAccountName** – toohello Especifica o nome da conta de armazenamento Olá fluxo NSG Olá contém logs que você deseja tooload e visualizar.
    1. **NumberOfLogFiles** – Especifica o número de saudação de arquivos de log que você deseja toodownload e visualizar no Power BI. Por exemplo, se for especificada a 50, Olá 50 arquivos de log mais recentes. FF temos 2 NSGs habilitado e configurado a conta de toothis toosend NSG fluxo de logs, hello últimas 25 horas de logs pode ser exibidas.

    ![principal do Power BI][2]

1. Digite hello chave de acesso para sua conta de armazenamento. Você pode encontrar as chaves de acesso válido navegando tooyour conta de armazenamento hello Azure portal e selecionando **chaves de acesso** no menu de configurações de saudação. Clique em **Conectar** e, em seguida, aplique as alterações.

    ![teclas de acesso][3]

    ![chave de acesso 2][4]

4.  Os logs são baixar e analisada e agora você pode utilizar visuais pré-criados hello.

## <a name="understanding-hello-visuals"></a>Noções básicas sobre visuais Olá

Fornecido em Olá modelo são um conjunto de elementos visuais que ajudam faz sentido de saudação dados NSG fluxo de Log. Olá imagens a seguir mostram um exemplo de qual painel Olá aparência quando preenchida com dados. Confira a seguir as informações detalhadas sobre cada visual 

![powerbi][5]
 
Talkers de parte superior do Hello visual mostra Olá IPs que iniciou Olá a maioria das conexões pela Olá período especificado. tamanho de saudação das caixas Olá corresponde número relativo de toohello de conexões. 

![toptalkers][6]

Hello, seguir gráficos de série de tempo mostram Olá número de fluxos em período de saudação. gráfico superior Olá segmentado por direção do fluxo de saudação e Olá inferior é segmentada por decisão Olá feita (permitir ou negar). Com esse visual, é possível examinar as tendências do tráfego ao longo do tempo e identificar picos anormais ou quedas no tráfego ou na segmentação de tráfego.

![flowsoverperiod][7]

Olá gráficos a seguir mostram Olá fluxos por interface de rede, com hello superior segmentadas por direção do fluxo e Olá inferior segmentadas por decisão tomada. Com essas informações, você pode obter ideias sobre que suas VMs comunicadas Olá tooothers relativo a maioria das e se o tráfego tooa VM específica está sendo permitido ou negado.

![flowspernic][8]

Olá gráfico de roda de rosca a seguir mostra uma divisão de fluxos de porta de destino. Com essas informações, você pode exibir as portas de destino Olá usado mais comumente usadas em Olá especificado período.

![donut][9]

Olá seguinte gráfico de barras mostra Olá fluxo NSG e regra. Com essas informações, você pode ver Olá NSGs responsáveis por hello mais tráfego e divisão de saudação do tráfego em um NSG pela regra.

![barchart][10]
 
Hello seguintes gráficos informativos exibe informações sobre Olá NSGs presente nos logs de saudação, Olá número de fluxos capturados por período hello e data de saudação de log mais antigo de Olá capturado. Essas informações lhe dá uma ideia do que os NSGs estão sendo registradas em log e Olá intervalo de datas de fluxos.

![infochart1][11]

![infochart2][12]

Esse modelo inclui Olá tooallow segmentações de dados a seguir você tooview somente Olá os dados que está mais interessados em. Você pode filtrar seus grupos de recursos, NSGs e regras. Você também pode filtrar em informações de 5 tuplas, a decisão e a hora de Olá Olá log foi gravado.

![slicers][13]

## <a name="conclusion"></a>Conclusão

Mostramos neste cenário que usando logs de fluxo de grupo de segurança de rede fornecidas pelo observador de rede e o Power BI, estamos toovisualize capaz e entender o tráfego de saudação. Usando o modelo de saudação fornecido, o Power BI baixa os logs de saudação diretamente do armazenamento e processa-os localmente. Modelo de saudação do tempo gasto tooload varia dependendo do número de saudação de arquivos solicitados e o tamanho total dos arquivos baixados.

Se sentir livre toocustomize este modelo para suas necessidades. Há várias maneiras de usar o Power BI com logs de fluxo do grupo de segurança de rede. 

## <a name="notes"></a>Observações

* Os logs, por padrão, são armazenados em `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Se houver outros dados em outro diretório eles Olá toopull consultas e dados de saudação do processo devem ser modificados.

* modelo de saudação fornecido não é recomendado para uso com mais de 1 GB de logs.

* Se você tiver uma quantidade grande de logs, recomendamos que estude uma solução que use outro tipo de armazenamento de dados, como o Data Lake ou o SQL server.

## <a name="next-steps"></a>Próximas etapas

Saiba como toovisualize seu fluxo NSG registra com hello Elastick pilha visitando [visualizar tooand de padrões de tráfego de rede de suas VMs usando ferramentas de software livre](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
