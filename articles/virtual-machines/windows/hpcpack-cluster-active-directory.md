---
title: aaaHPC pacote de cluster com o Active Directory do Azure | Microsoft Docs
description: Saiba como toointegrate uma 2016 do HPC Pack cluster no Azure com o Active Directory do Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Gerenciar um cluster HPC Pack no Azure usando o Azure Active Directory
O [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) dá suporte à integração com o [Azure AD](../../active-directory/index.md) (Azure Active Directory) para administradores que implantam um cluster HPC Pack no Azure.



Siga as etapas de saudação neste artigo para as seguintes tarefas de nível alto de saudação: 
* Integrar manualmente o cluster HPC Pack ao locatário do Azure AD
* Gerenciar e agendar trabalhos no cluster HPC Pack no Azure 

Integrar uma solução de cluster de HPC Pack com o Azure AD segue as etapas padrão toointegrate outros aplicativos e serviços. Este artigo pressupõe que você esteja familiarizado com o gerenciamento básico de usuários no Azure AD. Para obter mais informações e em segundo plano, consulte Olá [documentação do Active Directory do Azure](../../active-directory/index.md) e Olá seção a seguir.

## <a name="benefits-of-integration"></a>Vantagens da integração


Azure Active Directory (AD do Azure) é um multilocatário baseado em nuvem identidades e diretórios serviço de gerenciamento que fornece acesso de logon único (SSO) toocloud soluções.

Integração de um cluster de HPC Pack com o Azure AD pode ajudá-lo a atingir Olá seguintes metas:

* Remova controlador de domínio do Active Directory tradicional de saudação do cluster de HPC Pack hello. Isso pode ajudar a reduzir os custos de saudação de manutenção de cluster Olá se isso não é necessário para sua empresa e o processo de implantação de saudação acelerar.
* Aproveitar Olá benefícios que são colocados pelo AD do Azure a seguir:
    *   Logon único 
    *   Usando uma identidade do AD local para o cluster de HPC Pack Olá no Azure 

    ![Ambiente do Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Pré-requisitos
* **Cluster HPC Pack 2016 implantado em máquinas virtuais do Azure** - para obter as etapas, confira [Implantar um cluster HPC Pack 2016 no Azure](hpcpack-2016-cluster.md). Você precisa nome DNS de saudação do nó principal hello e credenciais de saudação de um administrador de cluster para concluir as etapas neste artigo hello.

  > [!NOTE]
  > Não há suporte à integração do Azure Active Directory nas versões do HPC Pack anteriores ao HPC Pack 2016.



* **Computador cliente** -você precisa de um Windows ou Windows Server cliente computador executado muito HPC Pack utilitários de cliente. Se você desejar somente toouse Olá HPC Pack portal web ou trabalhos de toosubmit da API REST, você pode usar qualquer computador cliente de sua escolha.

* **Utilitários de cliente do HPC Pack** -instalar utilitários de cliente do HPC Pack Olá no computador do cliente hello, usando o pacote de instalação gratuita Olá disponível da saudação Microsoft Download Center.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Etapa 1: Registrar o servidor de cluster HPC Olá com seu locatário do AD do Azure
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Clique em **do Active Directory** em Olá menus à esquerda e clique em diretório desejado de saudação em sua assinatura. Você deve ter recursos de tooaccess de permissão no diretório de saudação.
3. Clique em **Usuários** e verifique se há contas de usuário já criadas ou configuradas.
4. Clique em **Aplicativos** > **Adicionar** e clique em **Adicionar um aplicativo que minha organização está desenvolvendo**. Digite hello informações no Assistente de saudação a seguir:
    * **Nome** - HPCPackClusterServer
    * **Tipo** - selecione **Aplicativo Web e/ou API Web**
    * **URL de logon**- Olá URL base para o exemplo hello, por padrão`https://hpcserver`
    * **URI da ID do aplicativo** - `https://<Directory_name>/<application_name>`. Substituir `<Directory_name`> com hello nome completo do seu locatário do AD do Azure, por exemplo, `hpclocal.onmicrosoft.com`e substitua `<application_name>` com nome hello escolhido anteriormente.

5. Depois que o aplicativo hello foi adicionado, clique em **configurar**. Configure Olá propriedades a seguir:
    * Selecione **Sim** para **O aplicativo é multilocatário**
    * Selecione **Sim** para **usuário atribuição necessário tooaccess aplicativo**.

6. Clique em **Salvar**. Quando o salvamento for concluído, clique em **Gerenciar Manifesto**. Essa ação baixa o arquivo de JavaScript Object Notation (JSON). Editar saudação baixado manifesto Localizando Olá `appRoles` definindo e adicionando Olá função de aplicativo a seguir:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Salve o arquivo hello. No portal de saudação, clique em **gerenciar manifesto** > **carregar manifesto**. Em seguida, você pode carregar manifesto editado hello.
8. Clique em **Usuários**, selecione um usuário e clique em **Atribuir**. Atribua um usuário de toohello Olá funções disponíveis (HpcUsers ou HpcAdminMirror). Repita essa etapa com outros usuários no diretório de saudação. Para obter informações sobre os usuários de cluster, confira [Gerenciar usuários de cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).

   > [!NOTE] 
   > toomanage usuários, é recomendável usar folha de visualização do Azure Active Directory Olá em Olá [portal do Azure](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Etapa 2: Registrar o cliente de cluster HPC Olá com seu locatário do AD do Azure

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Clique em **do Active Directory** em Olá menus à esquerda e clique em diretório desejado de saudação em sua assinatura. Você deve ter recursos de tooaccess de permissão no diretório de saudação.
3. Clique em **Aplicativos** > **Adicionar** e clique em **Adicionar um aplicativo que minha organização está desenvolvendo**. Digite hello informações no Assistente de saudação a seguir:

    * **Nome** - HPCPackClusterClient
    * **Tipo** – selecione **Aplicativo Cliente Nativo**
    * **URI de redirecionamento** - `http://hpcclient`

4. Depois que o aplicativo hello foi adicionado, clique em **configurar**. Saudação de cópia **ID do cliente** valor e salve-o. Você precisará dele mais tarde ao configurar o aplicativo.

5. Em **permissões tooother aplicativos**, clique em **Adicionar aplicativo**. Pesquisar e adicionar o aplicativo de HpcPackClusterServer hello (criado na etapa 1).

6. Em Olá **permissões delegadas** lista suspensa, selecione **HpcClusterServer acesso**. Em seguida, clique em **Salvar**.


## <a name="step-3-configure-hello-hpc-cluster"></a>Etapa 3: Configurar o cluster HPC Olá

1. Conecte-se toohello HPC Pack 2016 o nó principal no Azure.

2. Inicie o HPC PowerShell.

3. Execute Olá comando a seguir:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    onde

    * `AADTenant`Especifica o nome do locatário do AD do Azure hello, como`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Especifica a ID do cliente Olá para o aplicativo hello criado na etapa 2.

4. Reinicie o serviço de HpcSchedulerStateful hello.

    Em um cluster com vários nós de cabeçalho, você pode executar Olá comandos do PowerShell a seguir na Olá nó principal tooswitch Olá réplica primária para o serviço de HpcSchedulerStateful hello:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Etapa 4: Gerenciar e enviar trabalhos de cliente Olá

utilitários de cliente tooinstall Olá HPC Pack em seu computador, baixe os arquivos de instalação HPC Pack 2016 (instalação completa) de saudação Microsoft Download Center. Quando você começar a instalação hello, escolha a opção de instalação de saudação para Olá **utilitários de cliente do HPC Pack**.

tooprepare Olá cliente computador, instale o certificado de Olá usado durante a [instalação de cluster HPC](hpcpack-2016-cluster.md) no computador do cliente de saudação. Usar o Windows padrão de certificado gerenciamento procedimentos tooinstall Olá certificado público toohello **certificados – usuário atual** > **autoridades de certificação raiz confiáveis** armazenar. 

Agora execute comandos do HPC Pack hello ou use toosubmit Olá GUI do Gerenciador de trabalho do HPC Pack e gerenciar trabalhos de cluster usando a conta de saudação do AD do Azure. Para opções de envio de trabalho, consulte [cluster de HPC enviar trabalhos tooan HPC Pack no Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Quando você tentar cluster de HPC Pack de toohello tooconnect no Azure para Olá primeira vez, uma janela pop-up será exibida. Insira seu toolog de credenciais do AD do Azure no. Olá token, em seguida, é armazenado em cache. Posterior cluster toohello de conexões no uso do Azure Olá token armazenado em cache, a menos que as alterações de autenticação ou hello armazenado em cache é limpo.
>
  
Por exemplo, depois de concluir as etapas anteriores hello, você pode consultar para trabalhos de um cliente local da seguinte maneira:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Cmdlets úteis para envio de trabalhos com a integração do Azure AD 

### <a name="manage-hello-local-token-cache"></a>Gerenciar o cache de token local Olá

HPC Pack 2016 fornece dois novos cmdlets do PowerShell HPC cache de token local toomanage hello. Esses cmdlets são úteis para envio de trabalhos de forma não interativa. Consulte Olá exemplo a seguir:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Definir credenciais hello para enviar trabalhos usando a conta de saudação do AD do Azure 

Às vezes, talvez você queira toorun trabalho de saudação em usuário de cluster HPC hello (para um cluster HPC ingressado no domínio, executar como um usuário de domínio; para um cluster HPC ingressado no domínio, executar como um usuário local no nó de cabeçalho Olá).

1. Use Olá credenciais de saudação tooset comandos a seguir:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Em seguida, envie o trabalho de saudação da seguinte maneira. Olá/tarefa do trabalho é executado em $localUser em nós de computação hello.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Se `–Credential` não for especificado com `Submit-HpcJob`, Olá trabalho ou tarefa é executado em um usuário mapeado local como Olá conta AD do Azure. (cluster HPC Olá cria um usuário local com o mesmo nome como Olá tarefa de saudação do AD do Azure conta toorun de saudação.)
    
3. Definir dados estendidos de saudação conta AD do Azure. Isso é útil ao executar um trabalho MPI em nós do Linux usando a conta de saudação do AD do Azure.

   * Definir dados estendidos para Olá própria conta do AD do Azure

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Definir dados estendidos e executar como usuário do cluster HPC
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

