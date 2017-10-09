---
title: "aaaHow você redirecionar dispositivos USB no Azure RemoteApp? | Microsoft Docs"
description: Saiba como redirecionamento de toouse para dispositivos USB no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Como redirecionar dispositivos USB no Azure RemoteApp?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Redirecionamento do dispositivo permite que os usuários a usar o computador do hello USB dispositivos anexados tootheir ou tablet com hello aplicativos no Azure RemoteApp. Por exemplo, se você compartilhou Skype por meio do Azure RemoteApp, os usuários precisam ter toouse capaz de toobe câmeras seu dispositivo.

Antes de ir adiante, certifique-se de ler informações de redirecionamento de USB Olá em [usando redirecionamento no Azure RemoteApp](remoteapp-redirection.md). No entanto Olá recomendado nusbdevicestoredirect:s: * não funcionará para webcams USB e pode não funcionar por algumas impressoras USB ou dispositivos de múltiplas funções USB. Por design e por motivos de segurança, hello Azure RemoteApp administrador tem tooenable redirecionamento por GUID de classe de dispositivo ou por ID de instância do dispositivo antes que os usuários podem usar esses dispositivos.

Embora este artigo trata de redirecionamento de câmera da web, você pode usar um impressoras USB semelhante abordagem tooredirect e outros dispositivos USB de múltiplas funções não são redirecionados pelos Olá **nusbdevicestoredirect:s:*** comando.

## <a name="redirection-options-for-usb-devices"></a>Opções de redirecionamento para dispositivos USB
O Azure RemoteApp usa mecanismos muito semelhantes para redirecionar os dispositivos USB como Olá aquelas disponíveis para os serviços de área de trabalho remota. Olá tecnologia subjacente permite que você escolher método de redirecionamento correto Olá para um determinado dispositivo, tooget Olá melhor de ambos de alto nível e o redirecionamento do dispositivo USB do RemoteFX usando Olá **usbdevicestoredirect:s:** comando. Há quatro elementos toothis comando:

| Ordem de processamento | Parâmetro | Descrição |
| --- | --- | --- |
| 1 |* |Seleciona todos os dispositivos que não são captados pelo redirecionamento de alto nível. Observação: por design, o * não funciona para webcams USB. |
| {GUID de classe do dispositivo} |Seleciona todos os dispositivos que correspondam a saudação especificada classe de instalação. | |
| USB\InstanceID |Seleciona um dispositivo USB especificado para Olá dada a ID de instância. | |
| 2 |-USB\Instance ID |Remove as configurações de redirecionamento de Olá para o dispositivo especificado hello. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Redirecionando um dispositivo USB usando o GUID de classe de dispositivo Olá
Há duas maneiras de classe de dispositivo toofind Olá GUID que pode ser usado para redirecionamento. 

Olá primeira opção é Olá toouse [tooVendors disponível para Classes de instalação do dispositivo System-Defined](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Escolha classe hello mais parecido com o computador local do hello dispositivo toohello anexado. Para câmeras digitais, isso pode ser uma classe de Dispositivo de Imagem ou de Dispositivo de Captura de Vídeo. Você precisará toodo experimentá-los com Olá dispositivo classes toofind Olá correto de classe GUID que funciona com hello localmente anexado dispositivo USB (no nosso webcam Olá maiusculas).

Uma opção de segundo hello, ou a melhor maneira é toofollow GUID de classe de dispositivo específico do toofind Olá estas etapas:

1. Abrir Olá Gerenciador de dispositivos, localizar dispositivo Olá que será redirecionado e clique duas vezes e, em seguida, abrir as propriedades de saudação.
   ![Olá abrir Gerenciador de dispositivos](./media/remoteapp-usbredir/ra-devicemanager.png)
2. Em Olá **detalhes** guia, selecione a propriedade Olá **Guid de classe**. valor de saudação que aparece é hello GUID de classe para esse tipo de dispositivo.
   ![Propriedades da câmera](./media/remoteapp-usbredir/ra-classguid.png)
3. Use valor de Guid de classe de saudação tooredirect dispositivos que correspondem a ele.

Por exemplo:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Você pode combinar vários redirecionamentos de dispositivo em Olá mesmo cmdlet. Por exemplo: armazenamento local tooredirect e USB web câmera, cmdlet tem esta aparência:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

Quando você definir o redirecionamento do dispositivo pela classe GUID todos os dispositivos que correspondem a classe GUID no hello especificado coleção são redirecionados. Por exemplo, se houver vários computadores na rede local Olá que têm Olá mesmo webcams USB, você pode executar um único cmdlet tooredirect todos webcams hello.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Redirecionando um dispositivo USB usando a ID de instância de dispositivo Olá
Se você quiser um controle mais refinado e deseja toocontrol redirecionamento por dispositivo, você pode usar o hello **USB\InstanceID** parâmetro de redirecionamento.

a parte mais difícil Olá desse método é Localizando ID de instância de dispositivo Olá USB Você vai precisar acessar toohello computador e dispositivo USB específico de saudação. Depois, siga estas etapas:

1. Habilitar o redirecionamento de dispositivo de saudação na sessão de área de trabalho remota conforme descrito em [como posso usar meus dispositivos e recursos em uma sessão de área de trabalho remota?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Abra uma Conexão de Área de Trabalho Remota e clique em **Mostrar Opções**.
3. Clique em **Salvar como** toosave Olá atual conexão tooan RDP arquivo de configurações.  
    ![Salvar configurações de saudação como um arquivo RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Escolha um nome de arquivo e um local, por exemplo, MyConnection.rdp e este PC\Documents e salvar arquivo hello.
5. Abra hello MyConnection.rdp arquivo usando um editor de texto e localizar a ID de instância de saudação do dispositivo Olá deseja tooredirect.

Agora, use o ID de instância de saudação em Olá cmdlet a seguir:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Ajude-nos a ajudar você
Você sabia que na adição toorating neste artigo e fazer comentários para baixo abaixo, você pode fazer alterações toohello artigo? Falta alguma coisa? Há algo errado? Escrevi algo que não ficou muito claro? Role para cima e clique em **Editar no GitHub** toomake alterações - aqueles virão toous para revisão e, em seguida, uma vez que saia neles, você verá suas alterações e aprimoramentos aqui.

