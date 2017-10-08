---
title: aaaConfigure um Azure conta executar como | Microsoft Docs
description: "Este tutorial orienta você através do uso de criação, teste e exemplo hello de autenticação de entidade de segurança na automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nome principal do serviço, setspn, autenticação do azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Autenticar runbooks com uma conta Executar como do Azure
Este artigo mostra como a conta no portal do Azure de saudação tooconfigure um objeto de automação do Azure. toodo assim, você pode usar Olá executar como conta recurso tooauthenticate runbooks gerenciar recursos no Gerenciador de recursos do Azure ou gerenciamento de serviços do Azure.

Quando você cria uma conta de automação em Olá portal do Azure, criar automaticamente duas contas:

* Uma conta Executar como. Essa conta cria uma entidade de serviço no Azure AD (Azure Active Directory) e um certificado. Ele também atribui Olá Colaborador acesso baseado em função RBAC (controle), que gerencia os recursos do Gerenciador de recursos por meio de runbooks.
* Uma conta Executar como clássica. Essa conta carrega um certificado de gerenciamento, que é usada toomanage gerenciamento de serviços ou recursos clássicos por meio de runbooks.

Criar uma conta simplifica o processo de saudação para você e ajuda a que iniciar rapidamente criando e implantando toosupport runbooks de automação a automação precisa.

Com contas Executar como e Executar como Clássica, você pode:

* Fornecem uma maneira padronizada tooauthenticate com o Azure ao gerenciar o Gerenciador de recursos ou recursos de gerenciamento de serviços de runbooks em Olá portal do Azure.
* Automatize o uso de saudação do runbooks global, o que você pode configurar alertas do Azure.

> [!NOTE]
> Olá [recurso de integração do Azure alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) com automação runbooks global exige uma conta de automação que é configurada com uma conta executar como e uma conta clássico executar como. Você pode selecionar uma conta de automação que já tenha definido as contas executar como e clássico executar como ou, você pode escolher toocreate uma nova conta de automação.
>  

Este artigo mostra como toocreate uma conta de automação da saudação portal do Azure, atualizar uma conta de automação usando o PowerShell do Azure, gerenciar a configuração de conta hello e autenticar em seus runbooks.

Antes de começar a criar uma conta de automação, ele é uma boa ideia toounderstand e considere Olá seguinte:

* Criar uma conta de automação não afeta as contas de automação, que você pode ter já criado em Olá clássico ou modelo de implantação do Gerenciador de recursos.
* processo de saudação funciona apenas para contas de automação que você cria no portal do Azure de saudação. Tentativa de toocreate uma conta de saudação portal clássico do Azure não replicar configuração Executar como conta hello.
* Se você já tiver runbooks e ativos (como agendas ou variáveis) em vigor toomanage os recursos clássicos e deseja tooauthenticate runbooks com hello nova clássico conta executar como, siga um destes procedimentos hello:

  * toocreate uma conta clássico executar como, siga as instruções de saudação na seção de "Gerenciando sua conta executar como" hello. 
  * tooupdate sua conta existente, use Olá PowerShell script na seção de "Atualizar sua conta de automação usando o PowerShell" hello.
* tooauthenticate usando Olá nova conta executar como e a conta de execução clássico como automação, você precisa toomodify seus runbooks existentes com hello código de exemplo fornecido na seção Olá [exemplos de código de autenticação](#authentication-code-examples).

    >[!NOTE]
    >Olá conta executar como é para autenticação com base nos recursos do Gerenciador de recursos usando Olá entidade de serviço baseada em certificado. Olá clássico executar como conta é para autenticação com base nos recursos de gerenciamento de serviço com um certificado de gerenciamento.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Criar uma conta de automação de saudação portal do Azure
Nesta seção, você pode criar uma conta de automação do Azure de saudação portal do Azure, que por sua vez, cria uma conta executar como e uma conta clássico executar como.

>[!NOTE]
>toocreate uma conta de automação, você deve ser um membro da função de administradores de serviço hello ou coadministrador da assinatura de saudação que está concedendo acesso toohello assinatura. Você também deve ser adicionado como instância de Active Directory da assinatura de toothat um usuário padrão. Olá conta não precisa toobe atribuído a uma função com privilégios.
>
>Se você não for um membro da instância do Active Directory da assinatura Olá antes que sejam adicionadas toohello função de coadministrador da assinatura hello, serão adicionados tooActive diretório como convidado. Nesse caso, você receberá um "você não tem permissões toocreate..." saudação de aviso **adicionar conta de automação** folha.
>
>Os usuários que foram adicionados a função de coadministrador toohello primeiro pode ser removida da instância do Active Directory da assinatura hello e adicionado novamente toomake-los como um usuário completo no Active Directory. tooverify essa situação de saudação **Active Directory do Azure** painel Olá portal do Azure, selecionando **usuários e grupos**, selecionando **todos os usuários** e, depois de selecionar usuário específico do Hello, selecionando **perfil**. Olá valor Olá **o tipo de usuário** atributo sob o perfil de usuários Olá não deve ser iguais **convidado**.
>

1. Entrar no portal do Azure com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação do toohello.

2. Selecione **Contas de Automação**.

3. Em Olá **contas de automação** folha, clique em **adicionar**.
Olá **adicionar conta de automação** folha é aberta.

 ![folha de "Adicionar conta de automação" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Se sua conta não é um membro da função de administradores de assinatura hello e coadministrador da assinatura hello, Olá aviso a seguir será exibida em Olá **adicionar conta de automação** folha:
   >
   >![Aviso Adicionar Conta de Automação](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. Em Olá **adicionar conta de automação** folha em Olá **nome** , digite um nome para sua nova conta de automação.

5. Se você tiver mais de uma assinatura, Olá a seguir:

    a. Em **assinatura**, especifique uma nova conta de saudação.

    b. Em **Grupo de Recursos**, clique em **Criar novo** ou **Usar existente**.

    c. Em **Local**, especifique um datacenter do Azure.

6. Em **Criar conta Executar como do Azure**, selecione **Sim**e clique em **Criar**.

   > [!NOTE]
   > Se você escolher não toocreate Olá conta executar como selecionando **não**, será exibida uma mensagem de aviso Olá **adicionar conta de automação** folha. Embora Olá conta é criada no hello portal do Azure, ele não tem uma identidade de autenticação correspondente dentro de sua clássico ou serviço de diretório de assinatura do Gerenciador de recursos. Consequentemente, a conta de saudação não tem tooresources nenhum acesso em sua assinatura. Este cenário impede que todos os runbooks que fazem referência a essa conta se autenticaquem e executem tarefas em recursos nesses modelos de implantação.
   >
   > ![Mensagem de aviso na folha de "Adicionar conta de automação" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > Além disso, como entidade de serviço Olá não é criada, função de Colaborador Olá não está atribuída.
   >

7. Enquanto o Azure cria a conta de automação hello, você pode acompanhar o progresso de saudação em **notificações** menu hello.

### <a name="resources"></a>Recursos
Quando a conta de automação de saudação é criada com êxito, vários recursos são criados automaticamente para você. recursos de saudação estão resumidos na Olá duas tabelas a seguir:

#### <a name="run-as-account-resources"></a>Recursos da conta Executar como

| Recurso | Descrição |
| --- | --- |
| Runbook AzureAutomationTutorial | Um runbook gráfico de exemplo que demonstra como tooauthenticate usando Olá conta executar como e obtém todos os recursos do Gerenciador de recursos de saudação. |
| Runbook do AzureAutomationTutorialScript | Um runbook do PowerShell de exemplo que demonstra como tooauthenticate usando Olá conta executar como e obtém todos os recursos do Gerenciador de recursos de saudação. |
| AzureRunAsCertificate | ativo de certificado da saudação que é criado automaticamente quando você criar uma conta de automação ou usar Olá seguinte script do PowerShell para uma conta existente. Olá certificado permite que você tooauthenticate com o Azure para que você possa gerenciar recursos do Gerenciador de recursos do Azure de runbooks. certificado de saudação tem um tempo de vida de um ano. |
| AzureRunAsConnection | ativo de conexão de saudação que é criado automaticamente quando você criar uma conta de automação ou usar o script do PowerShell Olá para uma conta existente. |

#### <a name="classic-run-as-account-resources"></a>Recursos de conta Executar como clássica

| Recurso | Descrição |
| --- | --- |
| Runbook do AzureClassicAutomationTutorial | Um exemplo de runbook gráfico que obtém todas as VMs de saudação que são criados usando o modelo de implantação clássico Olá em uma assinatura usando Olá clássico executar como conta (certificado) e grava status e nome VM hello. |
| Runbook do script AzureClassicAutomationTutorial | Um exemplo de runbook do PowerShell que obtém todos os Olá clássicas VMs em uma assinatura usando Olá clássico executar como conta (certificado) e, em seguida, grava Olá status e nome VM. |
| AzureClassicRunAsCertificate | ativo de certificado Olá criado automaticamente usar tooauthenticate com o Azure, para que você possa gerenciar recursos clássicos do Azure de runbooks. certificado de saudação tem um tempo de vida de um ano. |
| AzureClassicRunAsConnection | ativo de conexão criadas automaticamente Olá usar tooauthenticate com o Azure, para que você possa gerenciar recursos clássicos do Azure de runbooks. |

## <a name="verify-run-as-authentication"></a>Verificar a autenticação de Executar como
Execute um tooconfirm de teste pequena que pode autenticar com êxito usando Olá nova conta executar como.

1. No portal do Azure de Olá, abra conta de automação de saudação que você criou anteriormente.

2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.

3. Selecione Olá **AzureAutomationTutorialScript** runbook e, em seguida, clique em **iniciar** toostart Olá runbook. Olá eventos a seguir ocorre:
 * Um [trabalho de runbook](automation-runbook-execution.md) é criado, hello **trabalho** folha é exibida, e o status do trabalho Olá é exibido na Olá **resumo do trabalho** lado a lado.
 * status do trabalho Olá começa como **na fila**, indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível.
 * o status de saudação se torna **iniciando** quando um trabalhador declarações trabalho hello.
 * Olá status se torna **executando** quando Olá runbook é iniciado.
 * Quando a execução do trabalho de runbook Olá for concluída, você verá um status de **concluído**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.  
Olá **saída** folha é exibida, mostrando esse runbook Olá autenticado e retornou uma lista de todos os recursos disponíveis no grupo de recursos de saudação com êxito.

5. Olá fechar **saída** folha tooreturn toohello **resumo do trabalho** folha.

6. Olá fechar **resumo do trabalho** folha e Olá correspondente **AzureAutomationTutorialScript** folha do runbook.

## <a name="verify-classic-run-as-authentication"></a>Verificar a autenticação de Executar como Clássica
Executar um pequeno semelhante testar tooconfirm que você pode autenticar com êxito usando Olá nova clássico conta executar como.

1. No portal do Azure de Olá, abra conta de automação de saudação que você criou anteriormente.

2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.

3. Selecione Olá **AzureClassicAutomationTutorialScript** runbook e, em seguida, clique em **iniciar** muito iniciar runbook hello. Olá eventos a seguir ocorre:

 * Um [trabalho de runbook](automation-runbook-execution.md) é criado, hello **trabalho** folha é exibida, e o status do trabalho Olá é exibido na Olá **resumo do trabalho** lado a lado.
 * status do trabalho Olá começa como **na fila**, indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível.
 * o status de saudação se torna **iniciando** quando um trabalhador declarações trabalho hello.
 * Olá status se torna **executando** quando Olá runbook é iniciado.
 * Quando a execução do trabalho de runbook Olá for concluída, você verá um status de **concluído**.

    ![Teste de runbook da entidade de segurança](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee Olá resultados detalhados da saudação runbook, clique em Olá **saída** lado a lado.  
Olá **saída** folha é exibida, mostrando esse runbook Olá autenticado e retornou uma lista de todas as VMs clássicas na assinatura Olá com êxito.

5. Olá fechar **saída** folha tooreturn toohello **resumo do trabalho** folha.

6. Olá fechar **resumo do trabalho** folha e Olá correspondente **AzureAutomationTutorialScript** folha do runbook.

## <a name="managing-your-run-as-account"></a>Gerenciando a conta Executar como
Em algum momento antes de sua conta de automação expira, você precisará toorenew Olá certificado. Se você acredita que Olá conta executar como foi comprometida, você pode excluir e recriá-la. Esta seção discute como tooperform essas operações.

### <a name="self-signed-certificate-renewal"></a>Renovação do certificado autoassinado
Olá o certificado autoassinado que você criou para a conta executar como de saudação expira um ano da data de saudação da criação. Você pode renová-lo a qualquer momento antes que ele expire. Quando você renová-la, o certificado de válido atual Olá é retido tooensure que todos os runbooks que são enfileiradas até ou ativamente em execução e que pode autenticar com hello conta executar como, não são afetados negativamente. certificado Olá permanece válido até a data de expiração.

> [!NOTE]
> Se você tiver configurado seu toouse de conta executar como automação um certificado emitido por sua autoridade de certificação corporativa e você usar essa opção, o certificado corporativo de saudação será substituído por um certificado autoassinado.

Olá toorenew do certificado, Olá a seguir:

1. No portal do Azure de Olá, abra conta de automação de saudação.

2. Em Olá **conta de automação** folha em Olá **propriedades de conta** painel, em **configurações de conta**, selecione **contas executar como**.

    ![Painel de propriedades da conta de Automação](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou Olá clássico conta executar como que você deseja toorenew Olá certificado para.

4. Em Olá **propriedades** folha para Olá selecionada conta, clique em **Renovar certificado**.

    ![Renovar o certificado da conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Enquanto o certificado hello está sendo renovado, você pode acompanhar o progresso de saudação em **notificações** menu hello.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Excluir uma conta Executar como ou Executar como Clássica
Esta seção descreve como toodelete e crie novamente uma conta executar como ou clássico executar como. Ao executar esta ação, Olá conta de automação é mantida. Depois de excluir uma conta executar como ou clássico executar como, você poderá recriá-la em Olá portal do Azure.

1. No portal do Azure de Olá, abra conta de automação de saudação.

2. Em Olá **conta de automação** folha, no painel de propriedades da conta hello, selecione **contas executar como**.

3. Em Olá **contas executar como** folha de propriedades, selecione qualquer Olá executado como conta ou clássico executar como da conta que você deseja toodelete. Em seguida, na Olá **propriedades** folha para Olá selecionada conta, clique em **excluir**.

 ![Excluir Conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Enquanto a conta de hello está sendo excluída, você pode acompanhar o progresso de saudação em **notificações** menu hello.

5. Após a exclusão de conta hello, você pode criá-lo novamente no hello **contas executar como** opção de criação de folha de propriedades selecionando Olá **Azure conta executar como**.

 ![Recriar Olá automação executar como conta](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Configuração incorreta
Alguns itens de configuração necessárias para toofunction de conta executar como ou clássico executar como Olá corretamente podem foram excluídos ou incorretamente criados durante a instalação inicial. Olá itens incluem:

* Ativo de certificado
* Ativo de conexão
* Conta executar como foi removida da função de Colaborador Olá
* Entidade de serviço ou aplicativo no Azure AD

Olá anterior e outras instâncias de uma configuração incorreta, Olá conta de automação detecta Olá altera e exibe o status de *incompleta* em Olá **contas executar como** folha de propriedades para Olá conta.

![Status incompleto de configuração de conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Quando você selecionar a conta executar como do hello, Olá conta **propriedades** painel exibe o saudação a seguinte mensagem de erro:

![Mensagem de aviso incompleto da configuração da conta Executar como](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Rapidamente, você pode resolver esses problemas de conta executar como, excluindo e recriando conta hello.

## <a name="update-your-automation-account-by-using-powershell"></a>Atualizar sua conta de Automação usando o PowerShell
Você pode usar sua conta de automação existente de PowerShell tooupdate se:

* Criar uma conta de automação, mas recusar toocreate Olá executar como conta.
* Você já usa uma recursos de Gerenciador de recursos de toomanage de conta de automação e deseja tooupdate Olá tooinclude Olá executar como conta para autenticação de runbook.
* Você já usa uma automação conta toomanage os recursos clássicos e você deseja tooupdate-Olá toouse clássico executar como conta em vez de criar uma nova conta e migrar seu tooit runbooks e ativos.   
* Você quer toocreate executar como e uma conta clássico executar como usando um certificado emitido por sua autoridade de certificação (CA).

script Hello tem Olá pré-requisitos a seguir:

* script Hello pode ser executado somente no Windows 10 e Windows Server 2016 com módulos do Azure Resource Manager 2.01 e posteriores. Não há suporte nas versões anteriores do Windows.
* Azure PowerShell 1.0 e posterior. Para obter informações sobre versão Olá PowerShell 1.0, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* Uma conta de automação, que é referenciada como valor Olá Olá *– AutomationAccountName* e *- ApplicationDisplayName* parâmetros em Olá script do PowerShell a seguir.

Olá tooget valores para *SubscriptionID*, *ResourceGroup*, e *AutomationAccountName*, que são parâmetros obrigatórios para scripts hello, Olá a seguir:
1. No hello portal do Azure, selecione sua conta de automação Olá **conta de automação** folha e, em seguida, selecione **todas as configurações**. 
2. Em Olá **todas as configurações** folha, em **configurações de conta**, selecione **propriedades**. 
3. Observe os valores hello Olá **propriedades** folha.

![folha de "Propriedades" Hello automação conta](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Criar o script do PowerShell da conta Executar como
Este script do PowerShell inclui suporte para Olá configurações a seguir:

* Crie uma conta Executar como usando um certificado autoassinado.
* Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado.
* Crie uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo.
* Crie uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem do Azure governamental.

Dependendo da opção de configuração de saudação que selecionar script hello cria Olá itens a seguir.

**Para contas Executar como:**

* Cria um Azure AD aplicativo toobe exportado com a saudação autoassinada ou chave pública do certificado da empresa, cria uma conta de serviço principal para o aplicativo hello no AD do Azure e atribui Olá função Colaborador para conta Olá no seu atual assinatura. Você pode alterar essa configuração tooOwner ou qualquer outra função. Para obter mais informações, confira [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).
* Cria um ativo de certificado de automação chamado *AzureRunAsCertificate* em Olá especificado na conta de automação. ativo de certificado Olá mantém Olá chave privada do certificado que é usado pelo aplicativo hello AD do Azure.
* Cria um ativo de conexão de automação chamado *AzureRunAsConnection* em Olá especificado na conta de automação. ativo de conexão Olá mantém applicationId hello, tenantId, subscriptionId e a impressão digital do certificado.

**Para contas Executar como clássicas:**

* Cria um ativo de certificado de automação chamado *AzureClassicRunAsCertificate* em Olá especificado na conta de automação. ativo de certificado Olá mantém a chave privada do certificado Olá usado pelo certificado de gerenciamento de saudação.
* Cria um ativo de conexão de automação chamado *AzureClassicRunAsConnection* em Olá especificado na conta de automação. ativo de conexão Olá contém o nome da assinatura hello, subscriptionId e nome do ativo de certificado.

>[!NOTE]
> Se você selecionar a opção para criar uma conta clássico executar como, após a execução do script hello, carregamento Olá pública repositório de certificados gerenciamento de toohello (extensão de nome de arquivo. cer) para a assinatura de saudação que Olá conta de automação foi criado no.
> 

tooexecute Olá scripts e carregar certificado hello, Olá a seguir:

1. Salve Olá script a seguir em seu computador. Neste exemplo, salve-o com o nome de arquivo hello *RunAsAccount.ps1 novo*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. No computador, clique em **Iniciar** e inicie o **Windows PowerShell** com direitos de usuário elevados.

3. De saudação elevado shell de linha de comando do PowerShell, vá toohello pasta que contém o script hello criado na etapa 1.

4. Execute script hello usando valores de parâmetro de saudação para configuração Olá que precisar.

    **Criar uma conta Executar como usando um certificado autoassinado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado autoassinado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Criar uma conta Executar como e uma conta Executar como Clássica usando um certificado corporativo**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Criar uma conta executar como e uma conta clássico executar como usando um certificado autoassinado no hello nuvem Azure Government**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Depois que o script hello executado, será tooauthenticate solicitado com o Azure. Entrar com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.
    >
    >

Depois que o script hello foi executada com êxito, observe o seguinte Olá:
* Se você criou uma conta clássico executar como com um certificado autoassinado público (arquivo. cer), script hello cria e salva-a pasta de arquivos temporários toohello no computador em que o perfil de usuário Olá *%USERPROFILE%\AppData\Local\Temp*, que você usou a sessão do PowerShell Olá tooexecute.
* Se tiver criado uma conta Executar como Clássica com um certificado público corporativo (arquivo .cer), use este certificado. Siga as instruções de saudação de [carregar um certificado de API de gerenciamento toohello portal clássico do Azure](../azure-api-management-certs.md)e, em seguida, validar a configuração de credencial de saudação com recursos de gerenciamento de serviço usando Olá [código de exemplo tooauthenticate com recursos de gerenciamento do serviço](#sample-code-to-authenticate-with-service-management-resources). 
* Se você fez *não* criar uma conta clássico executar como, autenticar com recursos de Gerenciador de recursos e validar a configuração de credencial de saudação usando Olá [código para autenticar com o serviço de gerenciamento de exemplo recursos](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Tooauthenticate de código de exemplo com os recursos do Gerenciador de recursos
Você pode usar o seguinte Olá atualizado código de exemplo, obtido Olá *AzureAutomationTutorialScript* exemplo de runbook, tooauthenticate usando Olá executar como conta toomanage Gerenciador de recursos recursos com seus runbooks.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp você tooeasily de trabalho entre várias assinaturas, o script hello inclui duas linhas de código adicionais que dão suporte ao fazer referência a um contexto de assinatura. Um ativo variável denominado *SubscriptionId* contém Olá ID de assinatura de saudação. Depois de saudação `Add-AzureRmAccount` cmdlet instrução, Olá [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet é declarado com o conjunto de parâmetros de saudação *- SubscriptionId*. Se o nome da variável Olá é muito genérico, você pode revisá-lo tooinclude um prefixo ou usar outro toomake de convenção de nomenclatura-tooidentify mais fácil. Como alternativa, você pode usar o conjunto de parâmetros de saudação *- SubscriptionName* em vez de *- SubscriptionId* com um ativo de variável correspondente.

Olá cmdlet que você pode usar para autenticar no runbook hello, `Add-AzureRmAccount`, Olá usa *ServicePrincipalCertificate* conjunto de parâmetros. Ele autentica usando Olá serviço certificado principal, não as credenciais do usuário hello.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Tooauthenticate de código de exemplo com os recursos de gerenciamento de serviço
Você pode usar o hello após o código de exemplo atualizado, o que é obtido da saudação *AzureClassicAutomationTutorialScript* exemplo de runbook, tooauthenticate usando Olá clássico conta executar como toomanage recursos clássicos com seu runbooks.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Próximas etapas
* [Objetos de aplicativo e entidade de serviço no Azure AD](../active-directory/active-directory-application-objects.md)
* [Controle de acesso com base em função na Automação do Azure](automation-role-based-access-control.md)
* [Visão geral sobre certificados para os Serviços de Nuvem do Azure](../cloud-services/cloud-services-certs-create.md)
