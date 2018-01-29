---
title: Instale o PowerShell para a pilha do Azure | Microsoft Docs
description: Saiba como instalar o PowerShell para Azure pilha.
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: F8D99A91-15B5-4073-BE07-A43514A6D2CF
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: mabrigg
ms.openlocfilehash: b5cc53387b6867d776059856b6e7793abbc67c9a
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="install-powershell-for-azure-stack"></a>Instale o PowerShell para a pilha do Azure  

Pilha do Azure compatíveis módulos do PowerShell do Azure são necessárias para trabalhar com a pilha do Azure. Neste guia, vamos orientá-lo pelas etapas necessárias para instalar o PowerShell para Azure pilha. Você pode usar as etapas descritas neste artigo do Kit de desenvolvimento de pilha do Azure ou de um cliente externo baseado no Windows, se você estiver conectado por meio de VPN.

Este artigo possui instruções detalhadas para instalar o PowerShell para Azure pilha. No entanto, se você quiser instalar e configurar o PowerShell rapidamente, você pode usar o script que é fornecido no artigo "Colocar em funcionamento com o PowerShell". 

> [!NOTE]
> As etapas a seguir exigem o PowerShell 5.0. Para verificar a versão, execute $PSVersionTable.PSVersion e compare a versão "Principal".

Comandos do PowerShell para Azure pilha são instalados por meio da Galeria do PowerShell. Para registrar o repositório PSGallery, abra uma sessão do PowerShell com privilégios elevados do kit de desenvolvimento ou de um cliente externo baseado no Windows se você estiver conectado por meio de VPN e execute o seguinte comando:

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a>Desinstale as versões existentes do PowerShell

Antes de instalar a versão necessária, certifique-se de que você desinstale todos os módulos do PowerShell do Azure existentes. Você pode desinstalá-los usando um dos dois métodos a seguir:

* Para desinstalar os módulos do PowerShell existentes, entrar para o kit de desenvolvimento ou para o cliente externo baseado em Windows se você estiver planejando estabelecer uma conexão VPN. Feche todas as sessões ativas do PowerShell e execute o seguinte comando: 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* Entrar para o kit de desenvolvimento ou para o cliente externo baseado em Windows se você estiver planejando estabelecer uma conexão VPN. Excluir todas as pastas que começam com "Azure" do `C:\Program Files (x86)\WindowsPowerShell\Modules` e `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` pastas. A exclusão dessas pastas remove quaisquer módulos do PowerShell existentes dos escopos de usuário "global" e "AzureStackAdmin". 

As seções a seguir descrevem as etapas necessárias para instalar o PowerShell para Azure pilha. PowerShell pode ser instalado na pilha do Azure operado na conectado, parcialmente conectado, ou em um cenário desconectado. 

## <a name="install-powershell-in-a-connected-scenario-with-internet-connectivity"></a>Instale o PowerShell em um cenário conectado (com conectividade com a internet)

Módulos de AzureRM compatíveis pilha do Azure são instalados por meio de perfis de versão de API. A pilha do Azure requer o **2017-03-09-perfil** perfil de versão de API, que está disponível ao instalar o módulo AzureRM.Bootstrapper. Para saber mais sobre perfis de versão de API e os cmdlets fornecidos por elas, consulte o [gerenciar perfis de versão de API](azure-stack-version-profiles.md). Além dos módulos AzureRM, você também deve instalar os módulos do PowerShell de pilha específicos do Azure. Execute o seguinte script do PowerShell para instalar esses módulos em sua estação de trabalho de desenvolvimento:

> [!IMPORTANT]
> A versão do módulo do PowerShell AzureRM 1.2.11 vem com uma lista de alterações significativas. Para atualizar a partir de 1.2.10 versão, consulte o guia de migração em [https://aka.ms/azspowershellmigration](https://aka.ms/azspowershellmigration).

  ```powershell
  # Install the AzureRM.Bootstrapper module. Select Yes when prompted to install NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import the API Version Profile required by Azure Stack into the current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.11
  ```

Para confirmar a instalação, execute o seguinte comando:

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  Se a instalação for bem-sucedida, os módulos AzureRM e a pilha do Azure são exibidos na saída.

## <a name="install-powershell-in-a-disconnected-or-a-partially-connected-scenario-with-limited-internet-connectivity"></a>Instale o PowerShell em um cenário parcialmente conectado ou um desconectada (com conectividade de internet limitada)

Em um cenário parcialmente conectado ou desconectado, você deve primeiro baixar os módulos do PowerShell para um computador que tenha conectividade com a internet e transferi-los para o Kit de desenvolvimento de pilha do Azure para instalação.

> [!IMPORTANT]
> A versão do módulo do PowerShell AzureRM 1.2.11 vem com uma lista de alterações significativas. Para atualizar a partir de 1.2.10 versão, consulte o guia de migração em [https://aka.ms/azspowershellmigration](https://aka.ms/azspowershellmigration).

1. Entrar em um computador em que você tem conectividade com a internet e usa o script a seguir para baixar o AzureRM e AzureStack pacotes no computador local:

   ```powershell
   $Path = "<Path that is used to save the packages>"

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureRM `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.11

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureStack `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.11 
   ```

2. Copie os pacotes baixados em um dispositivo USB.

3. Entrar para o kit de desenvolvimento e copie os pacotes do dispositivo USB em um local no kit de desenvolvimento. 

4. Agora você deve registrar esse local como o repositório padrão e instalar os módulos AzureRM e AzureStack deste repositório:

   ```powershell
   $SourceLocation = "<Location on the development kit that contains the PowerShell packages>"
   $RepoName = "MyNuGetSource"

   Register-PSRepository `
     -Name $RepoName `
     -SourceLocation $SourceLocation `
     -InstallationPolicy Trusted

   ```powershell
   Install-Module AzureRM `
     -Repository $RepoName

   Install-Module AzureStack `
     -Repository $RepoName 
   ```

## <a name="next-steps"></a>Próximas etapas

* [Baixar ferramentas de pilha do Azure do GitHub](azure-stack-powershell-download.md)
* [Configurar o ambiente do PowerShell do usuário a pilha do Azure](azure-stack-powershell-configure-user.md)  
* [Gerenciar perfis de versão de API na pilha do Azure](azure-stack-version-profiles.md)  
