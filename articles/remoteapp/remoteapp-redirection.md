---
title: redirecionamento de aaaUsing no Azure RemoteApp | Microsoft Docs
description: Saiba como tooconfigure e usar redirecionamento no RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Usando o redirecionamento no RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Redirecionamento do dispositivo permite que os usuários interagem com aplicativos remotos usando o computador local do hello dispositivos anexados tootheir, telefone ou tablet. Por exemplo, se você tiver fornecido Skype por meio do Azure RemoteApp, o usuário precisa de câmera Olá instalada em seu toowork de PC com o Skype. Isso também é verdadeiro para impressoras, alto-falantes, monitores e uma variedade de periféricos conectados por USB.

RemoteApp aproveita Olá protocolo de área de trabalho remota (RDP) e RemoteFX tooprovide redirecionamento.

## <a name="what-redirection-is-enabled-by-default"></a>Qual redirecionamento está habilitado por padrão?
Quando você usa o RemoteApp, Olá redirecionamentos a seguir é habilitada por padrão. informações de saudação entre parênteses mostram a configuração de RDP de saudação.

* Tocar sons no computador local hello (**reproduzir neste computador**). (audiomode:i:0)
* Captura de áudio Olá computadores local e enviar toohello remoto (**gravar deste computador**). (audiocapturemode:i:1)
* Imprimir toolocal impressoras (redirectprinters:i:1)
* Portas COM (redirectcomports:i:1)
* Dispositivo de cartão inteligente (redirectsmartcards:i:1)
* Área de transferência (toocopy de capacidade e colar) (redirectclipboard:i:1)
* Suavização de fonte clear type (permitir suavização de fonte: i:1)
* Redirecionar todos os dispositivos Plug and Play com suporte. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>Quais são os outros redirecionamentos disponíveis?
Duas opções de redirecionamento estão desabilitadas por padrão:

* Redirecionamento de unidade (mapeamento da unidade): unidades do computador local se tornar unidades mapeadas na sessão remota hello. Isso permite que você salvar ou abrir arquivos de suas unidades locais enquanto você trabalha na sessão remota hello.
* Redirecionamento de USB: você pode usar o computador local do hello USB dispositivos anexados tooyour na sessão remota hello.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Alterar as configurações de redirecionamento no RemoteApp
Você pode alterar as configurações de redirecionamento de dispositivo Olá para uma coleção usando saudação do PowerShell do Microsoft Azure com o SDK. Depois de instalar Olá PowerShell novos e o SDK, primeiro configure toomanage sua assinatura como descrita em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

Em seguida, use um toohello semelhante do comando Propriedades RDP tooset Olá personalizadas a seguir:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Observe que  *`n*  é usado como um delimitador entre propriedades individuais.)

tooget uma lista de quais propriedades RDP personalizadas são configuradas, execute Olá cmdlet a seguir. Observe que as propriedades personalizadas somente são mostradas como resultados de saída e não Olá propriedades padrão:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Quando você define as propriedades personalizadas você deve especificar todas as propriedades personalizadas a cada hora; Caso contrário, a configuração de saudação reverte toodisabled.   

### <a name="common-examples"></a>Exemplos comuns
Use Olá redirecionamento de unidade tooenable cmdlet a seguir:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Use este cmdlet tooenable USB e unidade de redirecionamento:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Use esse compartilhamento de área de transferência do cmdlet toodisable:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Toocompletely se faça logoff de todos os usuários na coleção de saudação (e não apenas desconectá-los) antes de você testar a alteração de saudação. tooensure os usuários são completamente desconectados, vá toohello **sessões** guia na coleção de saudação no hello portal do Azure e logoff de todos os usuários que estão desconectados ou conectados. Às vezes, pode levar vários segundos para Olá unidades locais tooshow no Gerenciador de sessão hello.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Alterar as configurações de redirecionamento de USB no cliente do Windows
Se você quiser toouse redirecionamento de USB em um computador que se conecta tooRemoteApp, há 2 ações que precisam de toohappen. 1 - o administrador precisa de redirecionamento de USB tooenable no nível de coleção de saudação usando o PowerShell do Azure. 2 - em cada dispositivo em que você deseja que o redirecionamento de USB toouse, é necessário tooenable uma política de grupo que permite que ele. Esta etapa terá toobe feito para cada usuário que deseja toouse redirecionamento de USB.

> [!NOTE]
> O redirecionamento de USB com o RemoteApp do Azure só tem suporte para computadores com Windows.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Habilitar o redirecionamento de USB para Olá coleção do RemoteApp
Use Olá cmdlet tooenable redirecionamento de USB no nível de coleção Olá a seguir:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Habilitar o redirecionamento de USB para o computador de cliente Olá
configurações de redirecionamento de USB tooconfigure em seu computador:

1. Olá abrir Editor de diretiva de Grupo Local (GPEDIT. MSC). (Execute gpedit.msc no prompt de comando).
2. Abra **Configuração do Computador\Políticas\Modelos Administrativos\Componentes do Windows\Serviços da Área de Trabalho Remota\Cliente de Conexão da Área de Trabalho Remota\Redirecionamento de Dispositivo USB RemoteFX**.
3. Clique duas vezes em **Permitir redirecionamento de RDP de outros dispositivos USB RemoteFX com suporte deste computador**.
4. Selecione **habilitado**e, em seguida, selecione **administradores e usuários em Olá direitos de acesso de redirecionamento de USB do RemoteFX**.
5. Abra um prompt de comando com permissões administrativas e execute o comando a seguir de saudação:
   
        gpupdate /force
6. Reinicie o computador de saudação.

Você também pode usar o hello toocreate de ferramenta de gerenciamento de política de grupo e aplicar diretiva de redirecionamento de USB Olá para todos os computadores no seu domínio:

1. Faça logon no controlador de domínio Olá como administrador de domínio hello.
2. Olá abrir o Console de gerenciamento de diretiva de grupo. (Clique em **Iniciar > Ferramentas Administrativas > Gerenciamento de Política de Grupo**.)
3. Navegue toohello domínio ou unidade organizacional para o qual você deseja toocreate política de saudação.
4. Clique com o botão da direita do mouse em **Política de Domínio Padrão** e, em seguida, clique em **Editar**.
5. Abra **Configuração do Computador\Políticas\Modelos Administrativos\Componentes do Windows\Serviços da Área de Trabalho Remota\Cliente de Conexão da Área de Trabalho Remota\Redirecionamento de Dispositivo USB RemoteFX**.
6. Clique duas vezes em **Permitir redirecionamento de RDP de outros dispositivos USB RemoteFX com suporte deste computador**.
7. Selecione **habilitado**e, em seguida, selecione **administradores e usuários em Olá direitos de acesso de redirecionamento de USB do RemoteFX**.
8. Clique em **OK**.  

