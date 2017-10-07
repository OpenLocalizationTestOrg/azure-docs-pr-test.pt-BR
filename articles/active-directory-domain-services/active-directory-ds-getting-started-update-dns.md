---
title: "Serviços do Azure Active Directory domínio: Atualizar as configurações de DNS para Olá rede virtual do Azure | Microsoft Docs"
description: "Introdução aos Serviços de Domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Atualizar configurações de DNS para Olá rede virtual do Azure
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Tarefa 4: Atualizar as configurações de DNS para Olá rede virtual do Azure
Olá anterior tarefas de configuração, você habilitou com êxito do Azure Active Directory Domain Services para seu diretório. Olá próxima tarefa é tooensure que os computadores na rede virtual Olá podem se conectar e consumir esses serviços. Neste artigo, você pode atualizar configurações do servidor DNS Olá para sua rede virtual toopoint toohello dois endereços IP onde o Azure Active Directory Domain Services está disponível na rede virtual hello.

> [!NOTE]
> Depois de habilitar o Azure Active Directory Domain Services para o diretório de hello, observe endereços IP Olá para o Azure Active Directory Domain Services que são exibidos em Olá **configurar** guia de seu diretório.
>
>

configuração de servidor tooupdate Olá DNS para a rede virtual hello, no qual você habilitou os serviços de domínio Active Directory do Azure, a saudação concluir as etapas a seguir:

1. Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel esquerdo do hello, selecione **redes**.  
    Olá **redes** janela será aberta.

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. Em Olá **redes virtuais** guia, no qual você habilitou Azure Active Directory Domain Services tooview suas propriedades de rede virtual do hello select.
4. Clique em Olá **configurar** guia.

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. Em Olá **servidores DNS** seção, digite os endereços IP de saudação eram exibidos no hello **dos serviços de domínio** seção Olá **configurar** guia de seu diretório.
6. Clique em configurações do servidor DNS toosave Olá para essa rede virtual, no painel de tarefas de saudação na parte inferior da saudação da janela de saudação **salvar**.

   ![Atualizar configurações do servidor DNS Olá para rede virtual Olá](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Máquinas virtuais na rede Olá obter somente as novas configurações de DNS Olá após uma reinicialização. Se você precisar deles configurações de DNS tooget Olá atualizada imediatamente, disparar uma reinicialização do portal hello, PowerShell ou Olá CLI.
>
>

## <a name="next-steps"></a>Próximas etapas
Tarefa 5: [habilitar sincronização de senha tooAzure serviços de domínio do Active Directory](active-directory-ds-getting-started-password-sync.md)
