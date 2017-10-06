---
title: "aaaGet dados usando Olá API do Azure AD Reporting com certificados | Microsoft Docs"
description: "Explica como toouse Olá API do Azure AD relatórios com dados de tooget de credenciais do certificado de diretórios sem intervenção do usuário."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Obter dados usando a API de relatórios do AD do Azure Olá com certificados
Este artigo aborda como toouse Olá API do Azure AD relatórios com dados de tooget de credenciais do certificado de diretórios sem intervenção do usuário. 

## <a name="use-hello-azure-ad-reporting-api"></a>Use Olá API Reporting do AD do Azure 
API do Azure AD Reporting requer que você conclua Olá etapas a seguir:
 *  Instalar pré-requisitos
 *  Defina o certificado de saudação em seu aplicativo
 *  Obter um token de acesso
 *  Use Olá toocall token de acesso Olá API do Graph

Para saber mais sobre o código-fonte, confira [Aproveitar o módulo da API de Relatório](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils). 

### <a name="install-prerequisites"></a>Instalar pré-requisitos
Você precisará toohave V2 do PowerShell do Azure AD e o módulo AzureADUtils instalado.

1. Baixe e instale o Azure AD Powershell V2, seguindo as instruções de saudação em [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Baixar o módulo de utilitários do AD do Azure de saudação do [doWindows Azure/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Esse módulo fornece vários cmdlets do utilitário, incluindo:
   * versão mais recente de saudação do ADAL usando o Nuget
   * Tokens de acesso do usuário, chaves de aplicativo e certificados usando ADAL
   * Resultados paginados de manipulação da API do Graph

**módulo de utilitários do AD do Azure de saudação tooinstall:**

1. Criar um módulo de utilitários de saudação do diretório toosave (por exemplo, c:\azureAD) e baixar o módulo de saudação do GitHub.
2. Abra uma sessão do PowerShell e vá toohello diretório recém-criado. 
3. Importar o módulo hello e instale-o no caminho do módulo PowerShell hello usando o cmdlet Olá AzureADUtilsModule de instalação. 

sessão Olá deve parecer semelhante tela de toothis:

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Defina o certificado de saudação em seu aplicativo
1. Se você já tiver um aplicativo, obtenha sua ID de objeto de saudação Portal do Azure. 

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Abra uma sessão do PowerShell e conecte-se tooAzure AD usando o cmdlet Olá Connect-doWindows Azure.

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Use Olá AzureADApplicationCertificateCredential novo cmdlet de AzureADUtils tooadd um tooit de credenciais do certificado. 

>[!Note]
>Você precisa tooprovide Olá aplicativo ID de objeto que você capturou anteriormente, bem como Olá objeto de certificado (obter isso usando Olá Cert: unidade).
>


  ![Portal do Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Obter um token de acesso

tooget um token de acesso, use o cmdlet de Get-AzureADGraphAPIAccessTokenFromCert de saudação da AzureADUtils. 

>[!NOTE]
>É necessário toouse Olá ID do aplicativo em vez da saudação ID de objeto que você usou na última seção do hello.
>

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Use Olá toocall token de acesso Olá API do Graph

Agora você pode criar o script hello. Abaixo está um exemplo usando o cmdlet Invoke-AzureADGraphAPIQuery de saudação da saudação AzureADUtils. Esse cmdlet lida com várias páginas de resultados e, em seguida, envia o pipeline do PowerShell de toohello esses resultados. 

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

Você agora está pronto tooexport tooa CSV e salva tooa SIEM sistema. Você também pode quebrar seu script em uma tarefa agendada de tooget dados do AD do Azure do seu locatário periodicamente sem a necessidade de chaves do aplicativo toostore no código-fonte hello. 

## <a name="next-steps"></a>Próximas etapas
[conceitos básicos de saudação do gerenciamento de identidades do Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



