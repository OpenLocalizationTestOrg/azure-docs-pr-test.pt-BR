---
title: "serviços com o Visual Studio em nuvem aaaManaging funções no Azure | Microsoft Docs"
description: "Saiba como tooadd e remover funções no Azure cloud services com o Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Gerenciando funções nos serviços de nuvem do Azure com o Visual Studio
Depois que você criou seu serviço de nuvem do Azure, você pode adicionar novos tooit de funções ou remova funções existentes ele. Você também pode importar um projeto existente e convertê-la tooa função. Por exemplo, você pode importar um aplicativo Web ASP.NET e designá-lo como uma função web.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Adicionando um tooan de função serviço de nuvem do Azure
Olá etapas a seguir orientam você na adição de um web ou trabalho função tooan nuvem do Azure serviço projeto no Visual Studio.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, expanda o nó do projeto Olá

1. Saudação de atalho **funções** menu de contexto do nó toodisplay hello. No menu de contexto hello, selecione **adicionar**, em seguida, selecione uma função web existente ou uma função de trabalho na solução atual Olá ou criar um projeto de função web ou de trabalho. Também é possível selecionar um projeto apropriado, como um projeto de aplicativo Web ASP.NET e associá-lo a um projeto de função.

    ![Menu Opções tooadd um projeto de serviço de nuvem do Azure de tooan de função](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Removendo uma função de um serviço de nuvem do Azure
Olá etapas a seguir orientam você na remoção de uma função web ou de trabalho de um projeto de serviço de nuvem do Azure no Visual Studio.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, expanda o nó do projeto Olá

1. Expanda Olá **funções** nó.

1. Nó de Olá atalho deseja tooremove e, no menu de contexto hello, selecione **remover**. 

    ![Menu Opções tooadd um tooan de função serviço de nuvem do Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Lendo um projeto de serviço de nuvem do Azure de tooan de função
Se você remove uma função de seu projeto de serviço de nuvem, mas decide posteriormente função volta do tooadd Olá toohello projeto, somente a declaração de função hello e os atributos básicos, como pontos de extremidade e informações de diagnóstico, são adicionados. Não há recursos adicionais ou referências são adicionadas toohello `ServiceDefinition.csdef` arquivo ou toohello `ServiceConfiguration.cscfg` arquivo. Se você quiser tooadd essas informações, você precisa toomanually adicioná-lo de volta para esses arquivos.

Por exemplo, você pode remover uma função de serviço web e posteriormente decidir tooadd fazer essa função em sua solução. Se você fizer isso, ocorrerá um erro. tooprevent esse erro, ter Olá tooadd `<LocalResources>` elemento mostrado Olá seguir XML novamente no hello `ServiceDefinition.csdef` arquivo. Use o nome de função de serviço web de saudação que você adicionou no project hello como parte do atributo name Olá Olá Olá  **<LocalStorage>**  elemento. Neste exemplo, o nome de saudação da função de serviço da web hello é **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Próximas etapas
- [Configurar as funções de saudação para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
