---
title: "Início rápido da Central de Segurança do Azure – integrar seus computadores Windows à Central de Segurança | Microsoft Docs"
description: "Este guia de início rápido mostra como provisionar o Microsoft Monitoring Agent em um computador com Windows."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/07/2018
ms.author: terrylan
ms.openlocfilehash: 50cbbca9181d67bc41632a4650c76b9636a72356
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="quickstart-onboard-windows-computers-to-azure-security-center"></a>Início rápido: integrar computadores com Windows à Central de Segurança do Azure
Depois de integrar suas assinaturas do Azure, é possível habilitar a Central de Segurança para recursos sendo executados fora do Azure, por exemplo, no local ou em outras nuvens, por meio do provisionamento do Microsoft Monitoring Agent.

Este guia de início rápido mostra como instalar o Microsoft Monitoring Agent em um computador com Windows.

## <a name="prerequisites"></a>Pré-requisitos
Para começar a usar a Central de Segurança, você deve ter uma assinatura do Microsoft Azure. Se você não tiver uma assinatura, pode se inscrever em uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).

Você deverá estar no tipo de preço Standard da Central de Segurança antes de começar este guia de início rápido. Consulte [Integrar sua assinatura do Azure ao Centro de Segurança Standard](security-center-get-started.md) para obter instruções de atualização. Você pode experimentar a Central de Segurança Standard sem nenhum custo pelos primeiros 60 dias.

## <a name="add-new-windows-computer"></a>Adicionar novo computador com Windows

1. Faça logon no [Portal do Azure](https://azure.microsoft.com/features/azure-portal/).
2. No menu **Microsoft Azure**, selecione **Central de Segurança**. A **Central de Segurança – Visão geral** é aberta.

 ![Visão geral da Central de Segurança][2]

3. No menu principal da Central de Segurança, selecione **Integração à segurança avançada**.
4. Selecione **Você deseja adicionar computadores não Azure**.

   ![Integração à segurança avançada][3]

5. Em **Adicionar novos computadores não Azure**, é mostrada uma lista dos espaços de trabalho do Log Analytics. A lista inclui, se aplicável, o espaço de trabalho padrão criado para você pela Central de Segurança quando o provisionamento automático foi habilitado. Selecione esse espaço de trabalho ou outro que deseje usar.

    ![Adicionar computador não Azure][4]

  A folha **Agente Direto** abre com um link para baixar um agente do Windows e as chaves da sua ID do espaço de trabalho para ser usada na configuração do agente.

6.  Selecione o link **Baixar Agente do Windows** aplicável a seu tipo de processador do computador para baixar o arquivo de configuração.

7.  À direita da **ID do Espaço de Trabalho**, selecione o ícone copiar e cole a ID no Bloco de Notas.

8.  À direita da **Chave Primária**, clique no ícone copiar e cole a chave no Bloco de Notas.

## <a name="install-the-agent"></a>Instalar o agente
Agora você deve instalar o arquivo baixado no computador de destino.

1. Copie o arquivo para o computador de destino e execute a instalação.
2. Sobre o **boas-vindas** página, selecione **próxima**.
3. Na página **Termos de Licença**, leia a licença e selecione **Aceito**.
4. Na página **Pasta de Destino**, altere ou mantenha a pasta de instalação padrão e selecione **Avançar**.
5. Na página **Opções de Instalação do Agente**, escolha a opção de conectar o agente ao Azure Log Analytics (OMS) e selecione **Avançar**.
6. Na página **Azure Log Analytics**, cole a **ID do Espaço de Trabalho** e a **Chave do Espaço de Trabalho (Chave Primária)** que você copiou para o Bloco de Notas no procedimento anterior.
7. Caso o computador deva se reportar a um espaço de trabalho do Log Analytics na nuvem do Azure Governamental, selecione o formulário **Azure US Government** na lista suspensa do **Azure Cloud**.  Caso o computador precise se comunicar por meio de um servidor proxy ao serviço Log Analytics, selecione **Avançado** e forneça a URL e o número da porta do servidor proxy.
8. Selecione **Avançar** depois de ter terminado de fornecer as configurações necessárias.

  ![Instalar o agente][5]

9. Na página **Pronto para Instalar**, examine suas escolhas e selecione **Instalar**.
10. Na página **Configuração concluída com êxito**, selecione **Concluir**

Após concluir, o **Microsoft Monitoring Agent** aparecerá no **Painel de Controle**. Você pode revisar sua configuração e verificar se o agente está conectado.

Para obter mais informações sobre como instalar e configurar o agente, consulte [Conectar computadores com Windows](../log-analytics/log-analytics-agent-windows.md#install-the-agent-using-setup).

Agora você pode monitorar suas VMs do Azure e computadores não Azure em um único lugar. Em **Computação**, você tem uma visão geral de todas as VMs e computadores juntamente com recomendações. Cada coluna representa um conjunto de recomendações. A cor representa o estado de segurança atual da VM ou do computador para essa recomendação. A Central de Segurança também revela quaisquer detecções para esses computadores em alertas de segurança.

  ![Folha Computação][6]

Há dois tipos de ícones representados na folha **Computação**:

![icon1](./media/quick-onboard-windows-computer/security-center-monitoring-icon1.png) Computador não Azure

![icon2](./media/quick-onboard-windows-computer/security-center-monitoring-icon2.png) VM do Azure

## <a name="clean-up-resources"></a>Limpar recursos
Quando não for mais necessário, você poderá remover o agente do computador com Windows.

Para remover o agente:

1. Abra o **Painel de controle**.
2. Abra **Programas e Recursos**.
3. Em **Programas e Recursos**, selecione **Microsoft Monitoring Agent** e clique em **Desinstalar**.

## <a name="next-steps"></a>Próximas etapas
Neste guia de início rápido, você provisionou o Microsoft Monitoring Agent em um computador com Windows. Para saber mais sobre como usar a Central de Segurança, prossiga para o tutorial para configurar uma política de segurança e avaliar a segurança de seus recursos.

> [!div class="nextstepaction"]
> [Tutorial: Definir e avaliar as políticas de segurança](tutorial-security-policy.md)

<!--Image references-->
[2]: ./media/quick-onboard-windows-computer/overview.png
[3]: ./media/quick-onboard-windows-computer/onboard-windows-computer.png
[4]: ./media/quick-onboard-windows-computer/add-computer.png
[5]: ./media/quick-onboard-windows-computer/log-analytics-mma-setup-laworkspace.png
[6]: ./media/quick-onboard-windows-computer/compute.png
