---
title: "aaaEnable Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure | Microsoft Docs"
description: "Como tooconfigure do azure nuvem conexões de área de trabalho remota de tooallow aplicativo de serviço"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portal clássico do Azure](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Área de trabalho remota permite que você tooaccess área de trabalho de saudação de uma função em execução no Azure. Você pode usar um tootroubleshoot de conexão de área de trabalho remota e diagnosticar problemas com seu aplicativo enquanto ele está em execução.

Você pode habilitar uma conexão de área de trabalho remota na sua função durante o desenvolvimento, incluindo módulos de área de trabalho remota de saudação em sua definição de serviço ou você pode escolher tooenable área de trabalho remota por meio de saudação extensão de área de trabalho remota. Olá abordagem preferencial é toouse Olá área de trabalho remota extensão como você pode habilitar área de trabalho remota, mesmo após a implantação do aplicativo hello sem ter que tooredeploy seu aplicativo.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Configurar área de trabalho remota a partir do hello portal do Azure
Olá portal do Azure usa o método de extensão da área de trabalho remota de saudação para que você possa habilitar a área de trabalho remota mesmo após a implantação do aplicativo hello. Olá **área de trabalho remota** folha para seu serviço de nuvem permite que você tooenable área de trabalho remota, Olá alterar conta do administrador local usado tooconnect toohello VMs, certificado Olá usado na autenticação e defina Olá Data de expiração.

1. Clique em **serviços de nuvem**, clique em nome de Olá Olá do serviço de nuvem e, em seguida, clique em **área de trabalho remota**.

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Escolha se você deseja tooenable área de trabalho remota para uma função individual ou para todas as funções e altere o valor de saudação do alternador Olá muito**habilitado**.

3. Preencha os campos de saudação necessárias para o nome de usuário, senha, expiração e certificado.

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > Todas as instâncias de função serão reiniciadas quando você ativa área de trabalho remota pela primeira vez e clica em OK (marca de seleção). tooprevent uma reinicialização, a senha de Olá Olá certificado tooencrypt usado deve ser instalado na função hello. tooprevent uma reinicialização, [carregar um certificado para o serviço de nuvem Olá](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e, em seguida, retornar toothis caixa de diálogo.
   >
   >
3. Em **funções**, selecione função hello desejado tooupdate ou selecione **todos os** para todas as funções.

4. Ao concluir as atualizações da configuração, clique em **Salvar**. Levará alguns minutos antes que suas instâncias de função são conexões tooreceive pronto.

## <a name="remote-into-role-instances"></a>Remoto em instâncias de função
Depois que a área de trabalho remota está habilitada em funções hello, você pode iniciar uma conexão diretamente da saudação Portal do Azure:

1. Clique em **instâncias** tooopen Olá **instâncias** folha.
2. Selecione uma instância de função com a área de trabalho remota configurada.
3. Clique em **conectar** toodownload uma RDP de arquivo para a instância de função hello.

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Clique em **abrir** e **conectar** toostart Olá conexão de área de trabalho remota.

>[!NOTE]
> Se seu serviço de nuvem estiver atrás de um NSG, talvez seja necessário toocreate regras que permitam o tráfego em portas **3389** e **20000**.  A Área de Trabalho Remota usa a porta **3389**.  Instâncias de serviço de nuvem têm a carga balanceada, portanto diretamente, você não pode controlar quais tooconnect de instância para.  Olá *RemoteForwarder* e *RemoteAccess* agentes gerenciar o tráfego RDP e permitir Olá cliente toosend um cookie RDP e especifique um tooconnect instância individual para.  Olá *RemoteForwarder* e *RemoteAccess* agentes exigem essa porta **20000*** aberto, que pode ser bloqueado se você tiver um NSG.

## <a name="additional-resources"></a>Recursos adicionais

[Como tooConfigure serviços de nuvem](cloud-services-how-to-configure.md)
[serviços em nuvem perguntas Frequentes – área de trabalho remota](cloud-services-faq.md)
