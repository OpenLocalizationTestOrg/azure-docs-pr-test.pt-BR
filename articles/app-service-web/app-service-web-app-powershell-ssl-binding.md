---
title: "Certificados aaaSSL associação usando o PowerShell"
description: Saiba como toobind SSL certificados tooyour web app usando o PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Associação de certificado SSL do Serviço de Aplicativo do Azure usando o PowerShell
Com a versão de saudação do Microsoft Azure PowerShell versão 1.1.0 foi adicionado um novo cmdlet que daria Olá usuário Olá capacidade toobind nova ou existente SSL certificados tooan aplicativo Web existente.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sobre como usar o Gerenciador de recursos do Azure com base em toomanage de cmdlets do PowerShell do Azure sua seleção de aplicativos Web [Gerenciador de recursos do Azure com base em comandos do PowerShell para o aplicativo Web do Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Carregando e associando um novo certificado SSL
Cenário: usuário Olá que toobind um tooone de certificado SSL de seus aplicativos da web.

Saber o nome do grupo de recursos Olá que contém o aplicativo de web Olá, nome do aplicativo web hello, caminho do arquivo. pfx Olá certificado no computador do usuário Olá, Olá senha certificado hello e Olá nome do host personalizado, podemos usar o hello toocreate de comando do PowerShell a seguir que Associação de SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Observe que, antes de adicionar um aplicativo web de tooa de associação de SSL, você deve ter um nome de host (domínio personalizado) já configurado. Se o nome de host Olá não está configurado, você obterá um erro 'hostname' não existe durante a execução AzureRmWebAppSSLBinding de novo. Você pode adicionar um nome de host diretamente do portal de saudação ou usando o PowerShell do Azure. Hello seguinte trecho do PowerShell pode ser o nome de host do tooconfigure Olá antes de executar o New-AzureRmWebAppSSLBinding.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

É importante toounderstand que Olá cmdlet Set-AzureRmWebApp substitui Olá nomes de host para o aplicativo web de saudação. Portanto, Olá acima trecho do PowerShell estiver anexando lista existente de toohello Olá de nomes de host para o aplicativo web de saudação.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Carregando e associando um certificado SSL existente
Cenário: usuário Olá que toobind um tooone previamente carregado de certificado SSL de seus aplicativos da web.

Podemos obter lista de saudação de certificados já carregado tooa grupo de recursos específicos usando o comando a seguir de saudação

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Observe que os certificados Olá são tooa local específico local e grupo de recursos, hello usuário precisa carregar toore Olá certificado se o aplicativo de web de saudação configurado está em um local diferente e recurso grupo outros que de saudação necessário certificado 

Saber o nome do grupo de recursos Olá que contém o aplicativo de web hello, Olá nome do aplicativo web, Olá a impressão digital do certificado e Olá nome do host personalizado, podemos usar Olá toocreate de comando do PowerShell a seguir essa associação de SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Excluindo uma associação SSL existente
Cenário: usuário Olá que toodelete uma associação SSL existente.

Saber o nome do grupo de recursos Olá que contém o aplicativo de web hello, Olá nome do aplicativo web e Olá nome do host personalizado, podemos usar Olá tooremove de comando do PowerShell a seguir essa associação de SSL:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Observe que se Olá removido associação SSL foi Olá última associação usando esse certificado no local pelo certificado de saudação padrão será excluída, usuário Olá tookeep certificado de saudação ele pode usar o certificado de saudação do hello DeleteCertificate opção tookeep

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Referências
* [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)
* [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)
* [Usando o Azure PowerShell com o Gerenciador de Recursos do Azure](../powershell-azure-resource-manager.md)

