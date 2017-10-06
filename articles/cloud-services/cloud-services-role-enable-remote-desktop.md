---
title: "aaaEnable área de trabalho remota em um serviço de nuvem do Azure | Microsoft Docs"
description: "Como tooconfigure do azure nuvem conexões de área de trabalho remota de tooallow aplicativo de serviço"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portal clássico do Azure](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

Você pode habilitar uma conexão de área de trabalho remota na sua função durante o desenvolvimento, incluindo módulos de área de trabalho remota de saudação em sua definição de serviço ou você pode escolher tooenable área de trabalho remota por meio de saudação extensão de área de trabalho remota. Olá abordagem preferencial é toouse Olá área de trabalho remota extensão como você pode habilitar área de trabalho remota, mesmo após a implantação do aplicativo hello sem ter que tooredeploy seu aplicativo.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Configurar área de trabalho remota a partir do hello portal clássico do Azure
Olá portal clássico do Azure usa o método de extensão da área de trabalho remota de saudação para que você possa habilitar a área de trabalho remota mesmo após a implantação do aplicativo hello. Olá **configurar** página para seu serviço de nuvem permite que você tooenable área de trabalho remota, Olá alterar conta do administrador local usado tooconnect toohello VMs, certificado Olá usado na autenticação e defina Olá Data de expiração.

1. Clique em **serviços de nuvem**, clique em nome de Olá Olá do serviço de nuvem e, em seguida, clique em **configurar**.
2. Clique em Olá **remoto** botão na parte inferior da saudação.

    ![Serviços de nuvem remotos](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > Todas as instâncias de função serão reiniciadas quando você ativa área de trabalho remota pela primeira vez e clica em OK (marca de seleção). tooprevent uma reinicialização, a senha de Olá Olá certificado tooencrypt usado deve ser instalado na função hello. tooprevent uma reinicialização, [carregar um certificado para o serviço de nuvem Olá](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e, em seguida, retornar toothis caixa de diálogo.

3. Em **funções**, selecione função hello desejado tooupdate ou selecione **todos os** para todas as funções.
4. Faça uma saudação as seguintes alterações:

   * tooenable área de trabalho remota, selecione Olá **habilitar área de trabalho remota** caixa de seleção. toodisable área de trabalho remota, caixa de seleção Limpar hello.
   * Crie uma conta toouse em conexões de área de trabalho remota toohello instâncias de função.
   * Atualize a senha de saudação conta existente do hello.
   * Selecione um toouse certificado carregado para autenticação (carregamento Olá certificado usando **carregar** em Olá **certificados** página) ou criar um novo certificado.
   * Alterar a data de vencimento de saudação para configuração da área de trabalho remota de saudação.

5. Ao concluir as atualizações da configuração, clique em **OK** (marca de seleção).

## <a name="remote-into-role-instances"></a>Remoto em instâncias de função
Depois que a área de trabalho remota está habilitada em funções hello poderá remoto para uma instância de função por meio de várias ferramentas.

instância de função tooconnect tooa de saudação portal clássico do Azure:

1. Clique em **instâncias** tooopen Olá **instâncias** página.
2. Selecione uma instância de função com a área de trabalho remota configurada.
3. Clique em **conectar**e siga a área de trabalho da saudação tooopen Olá instruções.
4. Clique em **abrir** e **conectar** toostart Olá conexão de área de trabalho remota.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Use o Visual Studio tooremote em uma instância de função
No Visual Studio, Gerenciador de Servidores:

1. Expanda Olá **Azure** > **serviços de nuvem** > **[nome do serviço de nuvem]** nó.
2. Expanda **Preparo** ou **Produção**.
3. Expanda a função individual hello.
4. Uma das instâncias de função hello, clique **conectar usando a área de trabalho remota...** e, em seguida, digite Olá nome de usuário e senha.

![Área de trabalho remota do Gerenciador de Servidores](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>Use o arquivo RDP do PowerShell tooget Olá
Você pode usar o hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) arquivo RDP do cmdlet tooretrieve hello. Você pode usar o arquivo RDP de saudação com serviço de nuvem de saudação de tooaccess de Conexão de área de trabalho remota.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>Baixar o arquivo RDP de Olá por meio de saudação API de REST de gerenciamento de serviços programaticamente
Você pode usar o hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) arquivo RDP do REST operação toodownload hello.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>tooconfigure área de trabalho remota no arquivo de definição de serviço Olá
Esse método permite que você tooenable área de trabalho remota para o aplicativo hello durante o desenvolvimento. Essa abordagem requer senhas criptografadas armazenados em sua configuração de serviço de arquivo e qualquer configuração de área de trabalho remota do toohello atualizações exigem uma reimplantação do aplicativo hello. Se você quiser tooavoid essas desvantagens, você deve usar a extensão de área de trabalho remota Olá baseado abordagem descrita acima.  

Você pode usar o Visual Studio muito[habilitar uma conexão de área de trabalho remota](../vs-azure-tools-remote-desktop-roles.md) usando a abordagem de arquivo de definição de serviço hello.  
Olá etapas a seguir descrevem Olá alterações necessárias toohello serviço modelo arquivos tooenable área de trabalho remota. O Visual Studio fará automaticamente essas alterações durante a publicação.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Configurar conexão Olá no modelo de serviço Olá
Saudação de uso **Imports** saudação do elemento tooimport **RemoteAccess** módulo e hello **RemoteForwarder** módulo toohello [servicedefinition. Csdef](cloud-services-model-and-package.md#csdef) arquivo.

Olá arquivo de definição de serviço deve ser semelhante toohello seguinte exemplo com hello `<Imports>` elemento adicionado.

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
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
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
Olá [ServiceConfiguration](cloud-services-model-and-package.md#cscfg) arquivo deve ser semelhante toohello exemplo a seguir, observe Olá `<ConfigurationSettings>` e `<Certificates>` elementos. Olá certificado especificado deve ser [carregado o serviço de nuvem toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a>Recursos adicionais
[Como tooConfigure serviços de nuvem](cloud-services-how-to-configure.md)
[serviços em nuvem perguntas Frequentes – área de trabalho remota](cloud-services-faq.md)
