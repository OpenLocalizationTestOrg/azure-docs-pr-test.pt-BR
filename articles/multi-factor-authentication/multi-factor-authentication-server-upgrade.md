---
title: "atualização do servidor MFA aaaAzure | Microsoft Docs"
description: "As etapas e diretrizes tooupgrade Olá versão mais recente do servidor Azure multi-Factor Authentication tooa."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Atualizar toohello servidor mais recente do Azure multi-Factor Authentication

Este artigo orienta Olá processo de atualização v 6.0 do servidor Azure multi-Factor Authentication (MFA) ou superior. Se você precisar tooupgrade uma versão antiga do hello PhoneFactor Agent, consulte muito[atualização Olá agente PhoneFactor tooAzure servidor multi-Factor Authentication](multi-factor-authentication-get-started-server-upgrade.md).

Se você estiver atualizando a partir do V6. x ou toov7.x mais antiga ou mais recente, todos os componentes de alterar de too.NET 2.0 do .NET 4.5. Todos os componentes também exigem os Pacotes Redistribuíveis do Microsoft Visual C++ 2015 Atualização 1 ou posterior. instalador do servidor MFA Olá instala as versões x86 e x64 de saudação desses componentes se ainda não estiverem instalados. Se hello Portal do usuário e o serviço Web aplicativos móveis executados em servidores separados, você precisará tooinstall esses pacotes antes de atualizar esses componentes. Você pode pesquisar para a última atualização Microsoft Visual C++ 2015 redistribuível Olá em Olá [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Instalar a versão mais recente de saudação do servidor Azure MFA

1. Use instruções de saudação em [Download Olá servidor Azure multi-Factor Authentication](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget Olá última versão do hello servidor Azure MFA.
2. Faça um backup de arquivo de dados do servidor MFA Olá localizado em C:\Program programas\Servidor multi-Factor Authentication Server\Data\PhoneFactor.pfdata (assumindo Olá local padrão de instalação) em seu servidor mestre do MFA.
3. Se você executar vários servidores para alta disponibilidade, altere os sistemas de cliente Olá que autenticam toohello servidor MFA para que eles pararem de enviar tráfego toohello servidores que estão atualizando. Se você usar um balanceador de carga, remover um servidor de MFA de Balanceador de carga Olá Olá atualização e, em seguida, adicionar o servidor de saudação no farm de saudação.
4. Execute o instalador de novo de saudação em cada servidor MFA. Atualize os servidores subordinados primeiro porque eles podem ler Olá antigo arquivo de dados sendo replicado pelo mestre de saudação. 

  Não é necessário toouninstall servidor MFA atual antes de instalador de saudação em execução. instalador de saudação executa uma atualização in-loco. Olá caminho de instalação é obtido do registro de saudação da instalação anterior do hello, para que ele instala no hello mesmo local (por exemplo, C:\Program programas\Servidor multi-Factor Authentication Server). 
  
5. Se você for solicitado tooinstall um Microsoft Visual C++ 2015 Redistributable atualização pacote, aceite o prompt de saudação. Ambas as versões x86 e x64 de saudação do pacote de saudação são instaladas.
5. Se você usar Olá SDK do serviço Web, você será solicitado tooinstall Olá novo SDK do serviço Web. Quando você instala o hello novo SDK do serviço Web, verifique se esse nome de diretório virtual Olá coincide com o diretório virtual de saudação instalado anteriormente (por exemplo, MultiFactorAuthWebServiceSdk).
6. Repita as etapas de saudação em todos os servidores subordinados. Promova um dos Olá subordinados toobe Olá novo mestre, em seguida, servidor de mestre antiga atualização hello. 

## <a name="upgrade-hello-user-portal"></a>Atualizar Olá Portal do usuário

1. Faça um backup do arquivo Web. config Olá que está no diretório virtual de saudação do hello local de instalação do Portal do usuário (por exemplo, C:\inetpub\wwwroot\MultiFactorAuth). Se as alterações foram feitas toohello o tema padrão, faça um backup da pasta de App_Themes\Default Olá também. É melhor toocreate uma cópia da pasta de padrão de saudação e criar um novo tema que o tema padrão toochange hello.
2. Se Olá Portal do usuário é executado no mesmo servidor como Olá outros componentes do servidor MFA, Olá de saudação instalação do servidor MFA solicitará que você tooupdate Olá Portal do usuário. Aceite a solicitação de saudação e instalar a atualização do Portal do usuário hello. Verificar que esse nome de diretório virtual Olá corresponde a um diretório virtual de saudação instalado anteriormente (por exemplo, MultiFactorAuth).
3. Se for Olá Portal do usuário em seu próprio servidor, copie o arquivo de MultiFactorAuthenticationUserPortalSetup64.msi de saudação de saudação local de um dos servidores de MFA de saudação de instalação e colocá-lo no servidor de web do Portal do usuário hello. Execute o instalador de saudação. 

  Se um erro ocorrer informando, "Microsoft Visual C++ 2015 Redistributable atualização 1 ou superior é necessário," baixar e instalar o pacote de atualização mais recente Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/). Instale ambas as versões x86 e x64 de saudação.

4. Olá atualizado Portal do usuário software é instalado, compare o backup de Web. config de saudação criada na etapa 1 com o novo arquivo de Web. config hello. Se nenhum novos atributos existirem no Web. config de novo Olá, copie seu Web. config backup Olá toooverwrite de diretório virtual Olá uma nova. Outra opção é valores de appSettings Olá toocopy/colar e hello URL do SDK de serviço Web do arquivo de backup Olá para Web. config do hello novo.

Se você tiver Olá Portal do usuário em vários servidores, repetir a instalação de saudação em todos eles. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Atualizar Olá serviço Web aplicativos móveis

1. Faça um backup do arquivo Web. config Olá que está no diretório virtual de saudação do hello local de instalação do serviço Web aplicativos móveis (por exemplo, C:\inetpub\wwwroot\app ou C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Copie o arquivo de MultiFactorAuthenticationMobileAppWebServiceSetup64.msi de saudação de saudação local da saudação servidores MFA de instalação e colocá-lo no servidor de web de registro de aplicativo móvel hello.
3. Execute o instalador de saudação. 

  Se ocorrer um erro informando que o Microsoft Visual C++ 2015 Redistributable atualização 1 ou superior é necessária, baixe e instale o pacote de atualização mais recente da saudação da saudação [Microsoft Download Center](https://www.microsoft.com/download/). Instale ambas as versões x86 e x64 de saudação.

4. Depois de instala software do serviço Web aplicativos móveis Olá atualizado, compare Olá Web. config que foi feito o backup na etapa 1 com o novo arquivo de Web. config hello. Se não existe nenhum atributo de novo no Web. config de novo Olá, poderá copiar salvo Web. config no diretório virtual hello e substituir Olá uma nova. Outra opção é valores de appSettings Olá toocopy/colar e hello URL do SDK de serviço Web do arquivo de backup Olá para Web. config do hello novo.

Se você tiver Olá serviço Web aplicativos móveis em vários servidores, repetir a instalação de saudação em todos eles. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Atualizar Olá adaptadores do AD FS


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>Se o MFA for executado em servidores diferentes do que o AD FS

Essas instruções se aplicarão apenas se você executar o Servidor de Autenticação Multifator separadamente dos servidores do AD FS. Se ambos os serviços executados em Olá mesmos servidores, ignore esta seção e vá toohello etapas de instalação. 

1. Salvar uma cópia do arquivo multifactorauthenticationadfsadapter. config Olá que foi registrado no AD FS, ou exportar configuração hello usando Olá comando PowerShell a seguir: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. o nome do adaptador Olá é "WindowsAzureMultiFactorAuthentication" ou "AzureMfaServerAuthentication" dependendo da versão de hello instalada anteriormente.
2. Saudação de copiar arquivos a seguir Olá servidor MFA local toohello AD FS dos servidores de instalação:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Edite o script hello Register-multifactorauthenticationadfsadapter.ps1 adicionando `-ConfigurationFilePath [path]` toohello final de saudação `Register-AdfsAuthenticationProvider` comando. Substituir *[caminho]* com caminho completo de saudação toohello multifactorauthenticationadfsadapter. config arquivo ou arquivo de configuração de saudação exportado na etapa anterior hello. 

  Verificar atributos Olá Olá novo Multifactorauthenticationadfsadapter toosee se eles corresponderem a arquivo de configuração antigo hello. Se todos os atributos foram adicionados ou removidos na nova versão de hello, copiar os valores de atributo de saudação de toohello de arquivo de configuração antigo do hello uma nova ou modificar Olá antigo toomatch de arquivo de configuração.

### <a name="install-new-ad-fs-adapters"></a>Instalar novos adaptadores do AD FS

> [!IMPORTANT] 
> Os usuários não será necessário tooperform verificacao durante as etapas 3 a 8 desta seção. Se você tiver o AD FS configurado em vários clusters, você pode remover, Olá a atualização e a restauração de cada cluster Olá farm independentemente do tempo de inatividade de tooavoid outros clusters.

1. Remova alguns servidores do AD FS de saudação farm. Atualize esses servidores durante a saudação que outros ainda estão em execução.
2. Instale o novo adaptador de AD FS Olá em cada servidor removido do farm do hello AD FS. Se Olá servidor MFA é instalado em cada servidor do AD FS, você pode atualizar por meio de administração de servidor MFA Olá UX. Caso contrário, atualize executando MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  Se um erro ocorrer informando, "Microsoft Visual C++ 2015 Redistributable atualização 1 ou superior é necessário," baixar e instalar o pacote de atualização mais recente Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/). Instale ambas as versões x86 e x64 de saudação.

3. Vá muito**do AD FS** > **políticas de autenticação** > **Editar política de autenticação multifator Global**. Desmarque **WindowsAzureMultiFactorAuthentication** ou **AzureMFAServerAuthentication** (dependendo da versão atual do hello instalado). 

  Quando essa etapa for concluída, a verificação em duas etapas por meio do Servidor MFA não estará disponível neste cluster do AD FS após a conclusão da etapa 8.

4. Versão mais antiga de saudação de cancelamento de registro do adaptador do Olá AD FS, executando o script do PowerShell unregister-multifactorauthenticationadfsadapter.ps1 Olá. Certifique-se de que Olá *-nome* parâmetro ("WindowsAzureMultiFactorAuthentication" ou "AzureMFAServerAuthentication") faz a correspondência nome hello que foi exibido na etapa 3. Isso se aplica tooall servidores no cluster do hello mesmo AD FS porque não há uma configuração central.
5. Registre novo adaptador de AD FS Olá executando o script do PowerShell Register-multifactorauthenticationadfsadapter.ps1 hello. Isso se aplica tooall servidores no cluster do hello mesmo AD FS porque não há uma configuração central.
6. Saudação de reinicialização do serviço do AD FS em cada servidor removido do hello farm do AD FS.
7. Adicione servidores Olá atualizado fazer farm do toohello AD FS e remover Olá outros servidores do farm de saudação.
8. Vá muito**do AD FS** > **políticas de autenticação** > **Editar política de autenticação multifator Global**. Marque **AzureMfaServerAuthentication**.
9. Repita a etapa 2: servidores de Olá tooupdate agora é removidos do farm do hello AD FS e reinicie o serviço do hello AD FS nesses servidores.
10. Adicione os servidores no farm de saudação do AD FS.

## <a name="next-steps"></a>Próximas etapas

- Obtenha exemplos de [Cenários avançados com a Autenticação Multifator do Azure e VPNs de terceiros](multi-factor-authentication-advanced-vpn-configurations.md)

- [Sincronizar o Servidor MFA com o Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)

- [Configurar a Autenticação do Windows](multi-factor-authentication-get-started-server-windows.md) para os aplicativos
