---
title: "compilação de linha de aaaCommand do Azure | Microsoft Docs"
description: "Compilação de linha de comando do Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Compilando projetos do Azure da linha de comando Olá
Usando Olá Microsoft Build Engine (MSBuild), você pode criar produtos em ambientes de laboratório de compilação em que o Visual Studio não está instalado. O MSBuild usa um formato XML para arquivos de projeto extensíveis e com suporte total da Microsoft. Usando o formato de arquivo hello MSBuild, você pode descrever quais itens devem ser criados para uma ou mais plataformas e configurações.

Você também pode executar o MSBuild na linha de comando hello e este tópico descreve essa abordagem. Definindo propriedades na linha de comando hello, você pode criar configurações específicas de um projeto. Da mesma forma, você também pode definir destinos Olá compilações do MSBuild. Para saber mais sobre parâmetros de linha de comando e o MSBuild, confira [Referência de linha de comando MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>Parâmetros do MSBuild
toocreate de maneira mais simples de saudação um pacote é toorun MSBuild com hello `/t:Publish` opção. Por padrão, este comando cria um diretório na relação toohello pasta raiz do projeto Olá, como `<ProjectDirectory>\bin\Configuration\app.publish\`. Quando você compila um projeto do Azure, dois arquivos são gerados: Olá o próprio arquivo de pacote e o arquivo de configuração que acompanha hello:

* Arquivo de pacote (`project.cspkg`)
* Arquivo de configuração (`ServiceConfiguration.TargetProfile.cscfg`)

Por padrão, cada projeto do Azure inclui um arquivo de configuração de serviço para criações locais (depuração) e outro para criações na nuvem (preparo ou produção). No entanto, você pode adicionar ou remover arquivos de configuração de serviço conforme necessário. Quando você criar um pacote do Visual Studio, você será solicitado que tooinclude do arquivo de configuração de serviço junto com o pacote de saudação. Quando você criar um pacote usando o MSBuild, o arquivo de configuração do serviço local hello está incluído por padrão. arquivo tooinclude uma configuração de serviço diferente, Olá conjunto `TargetProfile` propriedade Olá comando MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Se você quiser toouse um diretório alternativo para Olá armazenados pacote e arquivos de configuração, definir o caminho de saudação usando Olá `/p:PublishDir=Directory\` opção, incluindo Olá separador de barra invertida à direita.

## <a name="next-steps"></a>Próximas etapas
Após a criação do pacote de saudação, você pode implantar tooAzure. Para obter um tutorial que demonstra como tooautomate esse processo, consulte [entrega contínua para serviços de nuvem no Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

