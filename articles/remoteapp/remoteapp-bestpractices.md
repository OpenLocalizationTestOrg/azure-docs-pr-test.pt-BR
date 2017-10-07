---
title: "práticas recomendadas do RemoteApp aaaAzure | Microsoft Docs"
description: "Práticas recomendadas para configurar e usar o RemoteApp do Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Práticas recomendadas para configurar e usar o RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) para obter detalhes.
> 
> 

Olá informações a seguir pode ajudá-lo a configurar e usar o Azure RemoteApp produtiva.

## <a name="connectivity"></a>Conectividade
* Sempre use a versão mais recente do cliente de saudação. Usar clientes mais antigos pode resultar em problemas de conectividade e outras experiências degradadas. Habilitar atualizações de aplicação automática para seu dispositivo garantirá o que cliente mais recente Olá é sempre instalado.
* Sempre use hello mais estável e confiável internet conexão disponível tooyou.  
* Use apenas conexões de proxy suportadas para desempenho ideal de conectividade.  Não há suporte para o proxy de meias para Hello.

## <a name="applications"></a>Aplicativos
* Salve e feche os aplicativos RemoteApp quando tiver terminado com o aplicativo hello. Não fechar o aplicativo hello pode resultar em perda de dados.
* Valide aplicativos personalizados antes de usá-los no RemoteApp do Azure. Isso inclui garantir que eles funcionam em uma plataforma de várias sessões e não consomem recursos desnecessários, como memória e CPU que pode enfraquecer o outro usuário Olá mesma coleção. Para obter informações, baixe e leia Olá [práticas recomendadas de compatibilidade de aplicativos para os serviços de área de trabalho remota](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Configuração e gerenciamento
* Manter suas imagens de modelo para cima toodate, instalar atualizações de software e outras correções críticas, conforme necessário. Isso garante que, como o Azure RemoteApp autoescalas toomeet sua capacidade, cada instância é corrigida.  
* Verifique se a sua implantação de serviços de Federação do Active Directory (AD FS) está segura e confiável. Caso contrário, as autenticações do cliente podem falhar, impedindo que os usuários acessem o RemoteApp do Azure.
* Configure imagens de modelo com aplicativos instalados, funções ou recursos que estão sem monitoramento do estado. Eles não devem confiar em todas as instâncias de máquinas virtuais de saudação em um serviço do RemoteApp está em um estado persistente.
  * Armazene todos os dados de usuário em perfis de usuário ou de outro serviço de toohello externo de locais de armazenamento, como local compartilhamentos de arquivos ou OneDrive.
  * Armazene dados compartilhados no serviço de toohello externo de locais de armazenamento, como local compartilhamentos de arquivos ou OneDrive.
  * Defina as configurações de todo o sistema na imagem de modelo de saudação em vez de em máquinas virtuais individuais em um serviço.
  * Desativar atualizações automáticas de software para aplicativos publicados - em vez disso, aplicá-las manualmente toohello imagem de modelo e testá-las antes de implantar o modelo de saudação.

