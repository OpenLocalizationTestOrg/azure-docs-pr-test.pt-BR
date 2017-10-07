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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Habilitar o Azure Active Directory Domain Services (Versão prévia)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Tarefa 4: atualizar as configurações de DNS para Olá rede virtual do Azure
Olá anterior tarefas de configuração, você habilitou com êxito do Azure Active Directory Domain Services para seu diretório. Olá próxima tarefa é tooensure que os computadores na rede virtual Olá podem se conectar e consumir esses serviços. Neste artigo, você pode atualizar configurações do servidor DNS Olá para sua rede virtual toopoint toohello dois endereços IP onde o Azure Active Directory Domain Services está disponível na rede virtual hello.

configuração de servidor tooupdate Olá DNS para a rede virtual hello, no qual você habilitou os serviços de domínio Active Directory do Azure, a saudação concluir as etapas a seguir:

1. Olá **visão geral** guia lista um conjunto de **necessárias etapas de configuração** toobe executada depois que o domínio gerenciado está totalmente provisionado. Olá a primeira etapa de configuração é **configurações do servidor de atualização de DNS para sua rede virtual**.

    ![Domain Services - guia Visão geral depois de totalmente provisionado](./media/getting-started/domain-services-provisioned-overview.png)

2. Quando o seu domínio está totalmente provisionado, dois endereços IP são exibidos neste bloco. Cada um do endereços IP representa um controlador de domínio para seu domínio gerenciado.

3. Olá toocopy primeiro IP endereço tooclipboard, clique em Olá cópia botão Avançar tooit. Em seguida, clique em Olá **servidores DNS configurar** botão.

4. Cole o endereço IP primeiro Olá a Olá **servidor DNS adicionar** textbox em Olá **servidores DNS** folha. Rolar horizontalmente toohello deixado toocopy Olá segundo endereço IP e cole-o em Olá **servidor DNS adicionar** caixa de texto.

    ![Domain Services- atualizar o DNS](./media/getting-started/domain-services-update-dns.png)

5. Clique em **salvar** quando você terminar de servidores DNS tooupdate Olá para rede virtual hello.

> [!NOTE]
> Máquinas virtuais na rede Olá obter somente as novas configurações de DNS Olá após uma reinicialização. Se você precisar deles configurações de DNS tooget Olá atualizada imediatamente, disparar uma reinicialização do portal hello, PowerShell ou Olá CLI.
>
>

## <a name="next-step"></a>Próxima etapa
[Tarefa 5: habilitar a sincronização de senha tooAzure serviços de domínio do Active Directory](active-directory-ds-getting-started-password-sync.md)
