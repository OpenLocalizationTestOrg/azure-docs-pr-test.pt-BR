---
title: "aaaHow tooSet de computador para o desenvolvimento de serviços de mídia com .NET"
description: "Saiba mais sobre os pré-requisitos de saudação do Media Services usando Olá SDK do Media Services para .NET. Saiba também como toocreate um aplicativo do Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>Desenvolvimento de serviços de mídia com o .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Este tópico discute como os serviços de mídia de toostart desenvolver aplicativos usando o .NET.

Olá **SDK do Azure Media Services .NET** biblioteca permite tooprogram em relação aos serviços de mídia usando o .NET. toomake mesmo toodevelop mais fácil com o .NET, hello **extensões do SDK do Azure Media Services .NET** biblioteca é fornecida. Esta biblioteca contém um conjunto de métodos de extensão e funções auxiliares simplificam o seu código .NET. As duas bibliotecas estão disponíveis por meio do **NuGet** e **GitHub**.

## <a name="prerequisites"></a>Pré-requisitos
* Uma conta de Serviços de Mídia em uma assinatura nova ou existente do Azure. Consulte o tópico Olá [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).
* Sistemas operacionais: Windows 10, Windows 7, Windows 2008 R2 ou Windows 8.
* .NET Framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio
Esta seção mostra como toocreate um projeto no Visual Studio e configurá-lo para o desenvolvimento de serviços de mídia.  Nesse caso, projeto de saudação é um aplicativo de console c# Windows, mas hello mesmas etapas de instalação mostradas aqui se aplicam tooother tipos de projetos, que você pode criar aplicativos de serviços de mídia (por exemplo, um aplicativo Windows Forms ou um aplicativo Web ASP.NET).

Esta seção mostra como toouse **NuGet** tooadd SDK do Media Services .NET extensões e outras bibliotecas dependentes.

Como alternativa, você pode obter os bits mais recentes do SDK do Media Services .NET de saudação do GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) ou [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilar solução hello e adicionar projeto de cliente de toohello Olá referências. Todas as dependências necessárias de saudação obtenham baixadas e extraídas automaticamente.

1. No Visual Studio, crie um novo aplicativo de console C#. Digite hello **nome**, **local**, e **nome da solução**e, em seguida, clique em Okey.
2. Compile a solução de saudação.
3. Use **NuGet** tooinstall e adicione **extensões do SDK do Azure Media Services .NET** (**windowsazure.mediaservices.extensions**). Instalar esse pacote também instala o **SDK do .NET dos Serviços de Mídia** e adiciona todas as outras dependências necessárias.
   
    Certifique-se de que você tem a versão mais recente de saudação do NuGet instalada. Para obter mais informações e instruções de instalação, consulte [NuGet](http://nuget.codeplex.com/).
4. No Gerenciador de soluções, clique o nome de saudação do projeto de saudação e escolha gerenciar pacotes do NuGet.
   
    caixa de diálogo Gerenciar pacotes NuGet Olá é exibida.
5. Na Galeria de Online hello, pesquisa de extensões de serviços de mídia do Azure, escolha as extensões de SDK .NET do serviços de mídia do Azure e clique em botão de instalar hello.
   
    projeto de saudação é modificado e referencia toohello extensões do SDK do Media Services .NET, SDK do Media Services .NET e outros assemblies dependentes são adicionados.
6. toopromote um ambiente de desenvolvimento mais limpo, considere habilitar a restauração de pacotes do NuGet. Para obter mais informações, consulte [Restauração do pacote NuGet"](http://docs.nuget.org/consume/package-restore).
7. Adicione uma referência muito**System. Configuration** assembly. Este assembly contém Olá System. Configuration. **ConfigurationManager** classe que é usada tooaccess arquivos de configuração (por exemplo, App. config).
   
    referências de tooadd usando a caixa de diálogo de referências de gerenciar Olá, com o botão direito em nome do projeto Olá no hello Gerenciador de soluções. Em seguida, selecione Adicionar e Referências.
   
    Olá Gerenciar referências aparecerá.
8. Em assemblies do .NET framework, localize e selecione o assembly System. Configuration de saudação e pressione Okey.
9. Abra o arquivo App. config de saudação e adicione um *appSettings* arquivo toohello de seção.     
   
    Definir valores de saudação que são necessárias tooconnect toohello API de serviços de mídia. Para obter mais informações, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). 

    Se você estiver usando [autenticação de usuário](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) seu arquivo de configuração será provavelmente têm valores para o seu domínio de locatário do AD do Azure e Olá ponto de extremidade de API de REST AMS.
    
    >[!Important]
    >A maioria dos exemplos de código Olá documentação do Azure Media Services definido, use um tipo de usuário (interativo) de autenticação tooconnect toohello AMS API. Esse método de autenticação funcionará bem para gerenciamento ou monitoramento de aplicativos nativos: aplicativos móveis, aplicativos do Windows e aplicativos de Console. Esse método de autenticação não é adequado para o servidor, serviços Web, tipo de aplicativos de APIs.  Para obter mais informações, consulte [Olá acesso AMS API com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Substituir existente Olá **usando** instruções no início de saudação do arquivo Program.cs Olá Olá código a seguir.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

Neste ponto, você está pronto toostart desenvolvendo um aplicativo de serviços de mídia.    

## <a name="example"></a>Exemplo

Aqui está um exemplo pequeno que se conecta toohello AMS API e lista todos os processadores de mídia disponíveis.
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>Próximas etapas

Agora [você pode se conectar toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) e iniciar [desenvolvendo](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

