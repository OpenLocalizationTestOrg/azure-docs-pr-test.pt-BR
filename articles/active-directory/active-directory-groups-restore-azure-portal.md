---
title: "grupo de aaaRestore um Office 365 excluído no Active Directory do Azure | Microsoft Docs"
description: "Como toorestore um grupo excluído, exibir restauráveis grupos e permamnently excluir um grupo no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Restaurar um grupo do Office 365 excluído na visualização do Azure Active Directory

Quando você exclui um grupo do Office 365 em hello Azure Active Directory (AD do Azure), o grupo de saudação excluído é retido, mas não é visível por 30 dias da data de exclusão de saudação. Isso é para que o grupo de saudação e seu conteúdo pode ser restaurado se necessário. Essa funcionalidade é restrita exclusivamente tooOffice 365 grupos no AD do Azure. Ele não fica disponível para grupos de segurança e de distribuição.

> [!NOTE] 
> Não use `Remove-MsolGroup` porque ele limpa grupo Olá permanentemente. Sempre use `Remove-AzureADMSGroup` toodelete um O365 grupo. 

permissões de saudação necessárias toorestore um grupo pode ser qualquer um dos seguintes hello:

Função  | Permissões 
--------- | ---------
Administrador da Empresa, suporte de Camada 2 do Parceiro e Administradores de Serviço do InTune | Pode restaurar qualquer grupo do Office 365 excluído 
Administrador da Conta de Usuário e suporte de Camada 1 do Parceiro | Pode restaurar qualquer grupo excluído do Office 365 exceto esses toohello atribuído a função de administrador da empresa 
Usuário | Pode restaurar qualquer grupo do Office 365 excluído que era propriedade dele 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Saudação de exibição excluído grupos do Office 365 que estão disponível toorestore
Olá cmdlets a seguir pode ser usado tooview Olá excluído grupos tooverify que Olá um ou os em que você estiver interessado não ainda foram permanentemente removidos. Esses cmdlets são parte da saudação [módulo PowerShell do AD do Azure](https://www.powershellgallery.com/packages/AzureAD/). Para obter mais informações sobre esse módulo podem ser encontradas no hello [versão 2 do Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0) artigo.

1.  Execute Olá cmdlet excluído toodisplay todos os grupos do Office 365 em seu locatário que estão disponível ainda toorestore a seguir.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Como alternativa, se você souber objectID Olá de um grupo específico (e você pode obtê-lo do hello cmdlet na etapa 1), execução Olá tooverify cmdlet que Olá grupo excluído específico a seguir não ainda foi permanentemente removido.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Como toorestore o grupo excluído do Office 365
Depois que você verificou que grupo Olá é toorestore disponível ainda, restaure o grupo de saudação excluído com uma saudação etapas a seguir. Se o grupo Olá contém documentos, sites de SP ou outros objetos persistentes, pode levar até too24 horas toofully restaurar um grupo e seu conteúdo.

1.  Execução hello seguinte grupo de saudação do cmdlet toorestore e seu conteúdo.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

Como alternativa, hello cmdlet a seguir pode ser executado toopermanently remover grupo de saudação excluído.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>Como saber se isso funcionou?
tooverify que você tenha restaurado com êxito um grupo do Office 365, executar Olá `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay informações sobre o grupo de saudação. Após a restauração de saudação solicitação é concluída:
- grupo de saudação será exibido na barra de navegação à esquerda de saudação do Exchange
- plano Olá para o grupo de hello serão exibidos no planejador
- Os sites do Sharepoint e todo o seu conteúdo estarão disponíveis
- Olá grupo pode ser acessado de qualquer um dos pontos de extremidade de troca de saudação e outras cargas de trabalho do Office 365 que dão suporte a grupos do Office 365


## <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre grupos do Azure Active Directory.

* [Consultar grupos existentes](active-directory-groups-view-azure-portal.md)
* [Gerenciar configurações de um grupo](active-directory-groups-settings-azure-portal.md)
* [Gerenciar membros de um grupo](active-directory-groups-members-azure-portal.md)
* [Gerenciar associações de um grupo](active-directory-groups-membership-azure-portal.md)
* [Gerenciar regras dinâmicas para usuários em um grupo](active-directory-groups-dynamic-membership-azure-portal.md)
