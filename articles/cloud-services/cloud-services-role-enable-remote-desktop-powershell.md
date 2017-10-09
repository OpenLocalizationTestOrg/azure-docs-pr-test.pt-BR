---
title: "aaaEnable Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure usando o PowerShell"
description: "Como tooconfigure do azure nuvem usando conexões de área de trabalho remota do PowerShell tooallow do aplicativo de serviço"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Habilitar a Conexão de Área de Trabalho Remota para uma função nos serviços de nuvem do Azure usando o PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portal clássico do Azure](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Área de trabalho remota permite que você tooaccess área de trabalho de saudação de uma função em execução no Azure. Você pode usar um tootroubleshoot de conexão de área de trabalho remota e diagnosticar problemas com seu aplicativo enquanto ele está em execução.

Este artigo descreve como tooenable área de trabalho remota em suas funções de serviço de nuvem usando o PowerShell. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) pré-requisitos Olá necessários para este artigo. PowerShell utiliza Olá extensão de área de trabalho remota para que você possa habilitar a área de trabalho remota após a implantação do aplicativo hello.

## <a name="configure-remote-desktop-from-powershell"></a>Configurar a Área de Trabalho Remota por meio do PowerShell
Olá [AzureServiceRemoteDesktopExtension conjunto](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet permite tooenable área de trabalho remota em funções especificadas ou todas as funções de sua implantação do serviço de nuvem. Olá cmdlet permite que você especifique hello nome de usuário e senha de usuário de desktop remoto Olá por meio de saudação *credencial* parâmetro que aceita um objeto PSCredential.

Se você estiver usando o PowerShell interativamente, você pode definir facilmente objeto PSCredential de saudação por chamada hello [Get-credenciais](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

```
$remoteusercredentials = Get-Credential
```

Este comando exibe uma caixa de diálogo que permite a você tooenter Olá nome de usuário e senha do usuário remoto Olá de forma segura.

Desde que o PowerShell Ajuda em cenários de automação, você também pode configurar Olá **PSCredential** objeto de forma que não exige interação do usuário. Primeiro, é necessário tooset uma senha segura. Começar com a especificação de uma senha de texto sem formatação convertê-lo a cadeia de caracteres segura tooa usando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). Em seguida você precisa tooconvert essa cadeia de caracteres segura em uma cadeia de caracteres criptografada padrão usando [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx). Agora você pode salvar esse arquivo de tooa de cadeia de caracteres criptografada padrão usando [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).

Você também pode criar um arquivo de senha segura para que você não tenha tootype senha Olá sempre. Além disso, um arquivo de senha segura é melhor do que um arquivo de texto sem formatação. Use Olá PowerShell toocreate um arquivo de senha de segurança a seguir:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Ao definir senha Olá, certifique-se de que você atenda aos Olá [requisitos de complexidade](https://technet.microsoft.com/library/cc786468.aspx).
>
>

objeto de credencial toocreate saudação do arquivo de senha segura hello, você deve ler o conteúdo do arquivo hello e convertê-los tooa back proteger a cadeia de caracteres usando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Olá [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet também aceita um *validade* parâmetro, que especifica um **DateTime** nos quais o usuário Olá vencimento da conta. Por exemplo, você pode definir Olá conta tooexpire alguns dias da saudação data e hora atuais.

Este exemplo do PowerShell mostra como tooset Olá extensão de área de trabalho remota em um serviço de nuvem:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
Você também pode especificar slot de implantação hello e funções que você deseja tooenable área de trabalho remota no. Se esses parâmetros não forem especificados, Olá habilita a área de trabalho remota em todas as funções hello **produção** slot de implantação.

Olá extensão da área de trabalho remota está associado uma implantação. Se você criar uma nova implantação do serviço de hello, você tem a área de trabalho remota tooenable em que a implantação. Se você desejar toohave área de trabalho remota habilitada, você deve considerar a integração de scripts do PowerShell Olá ao seu fluxo de trabalho de implantação.

## <a name="remote-desktop-into-a-role-instance"></a>Área de Trabalho Remota em uma instância de função
Olá [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet é usado tooremote a área de trabalho em uma instância de função específica do seu serviço de nuvem. Você pode usar o hello *LocalPath* Olá toodownload de parâmetro RDP arquivo localmente. Ou você pode usar o hello *iniciar* tooaccess de caixa de diálogo de Conexão de área de trabalho remota parâmetro toodirectly inicialização Olá Olá instância de função do serviço de nuvem.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Verifique se a extensão de Área de Trabalho Remota está habilitada em um serviço
Olá [AzureServiceRemoteDesktopExtension Get](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet exibe que área de trabalho remota está habilitada ou desabilitada em uma implantação de serviço. Olá cmdlet retorna o nome de usuário de saudação de usuário da área de trabalho remota hello e funções Olá Olá extensão de área de trabalho remota está habilitada para. Por padrão, isso ocorre no slot de implantação hello e você pode escolher Olá toouse em vez disso, o slot de preparo.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Remover a extensão de Área de Trabalho Remota de um serviço
Se você tiver habilitado a extensão de área de trabalho remota Olá em uma implantação e precisa tooupdate Olá configurações de área de trabalho remota, primeiro remova a extensão hello. E habilitá-lo novamente com novas configurações de saudação. Por exemplo, se você quiser tooset uma nova senha para a conta de usuário remoto hello ou Olá conta expirou. Isso é necessário nas implantações existentes que têm Olá extensão da área de trabalho remota habilitada. Para novas implantações, você pode simplesmente aplicar extensão Olá diretamente.

tooremove Olá remoto da área de trabalho extensão da implantação hello, você pode usar o hello [AzureServiceRemoteDesktopExtension remover](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet. Você pode especificar também slot de implantação de saudação e a função da qual você deseja que a extensão da área de trabalho remota do tooremove Olá.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> configuração de extensão do toocompletely remover hello, você deve chamar hello *remover* cmdlet com hello **UninstallConfiguration** parâmetro.
>
> Olá **UninstallConfiguration** parâmetro desinstala qualquer configuração de extensão que é o serviço toohello aplicado. Todas as configurações de extensão está associada a configuração do serviço hello. Olá chamada *remover* cmdlet sem **UninstallConfiguration** desassocia Olá <mark>implantação</mark> da configuração de extensão hello, assim, removendo efetivamente extensão de saudação. No entanto, a configuração da extensão Olá permanece associada ao serviço de saudação.
>
>

## <a name="additional-resources"></a>Recursos adicionais

[Como tooConfigure serviços de nuvem](cloud-services-how-to-configure.md)
[serviços em nuvem perguntas Frequentes – área de trabalho remota](cloud-services-faq.md)
