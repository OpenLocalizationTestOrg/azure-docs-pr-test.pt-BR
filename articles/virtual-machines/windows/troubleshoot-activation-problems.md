---
title: "aaaTroubleshoot problemas de ativação de máquina virtual Windows no Azure | Microsoft Docs"
description: "Fornece Olá solucionar as etapas para corrigir problemas de ativação de máquina virtual do Windows no Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Solucionar problemas de ativação de máquina virtual do Windows Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Se você tiver problemas durante a ativação do Azure máquina virtual do Windows (VM) que é criada a partir de uma imagem personalizada, você pode usar informações de saudação fornecidas nesta edição do documento tootroubleshoot hello. 

## <a name="symptom"></a>Sintoma

Quando você tenta tooactivate uma VM do Windows Azure, você recebe um erro de mensagem é semelhante a saudação de exemplo a seguir:

**Erro: Olá 0xC004F074 LicensingService de Software relatado que computador Olá não pôde ser ativado. Não foi possível fazer contato com nenhum Serviço de Gerenciamento de Chaves (KMS). Consulte Olá Log de eventos do aplicativo para obter informações adicionais.**

## <a name="cause"></a>Causa
Em geral, problemas de ativação da máquina virtual do Azure ocorrerem se Olá VM do Windows não está configurado por usando Olá a chave de instalação de cliente KMS adequada ou Olá VM do Windows tem um problema de conectividade toohello serviço KMS do Azure (kms.core.windows.net, porta 1668). 

## <a name="solution"></a>Solução

>[!NOTE]
>Se você estiver usando uma VPN site a site e forçada de túneis, consulte [Use Azure personalizado roteia a ativação do KMS tooenable com túnel forçado](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>Se você estiver usando o rota expressa e você tiver uma rota padrão publicados, consulte [VM do Azure pode falhar tooactivate ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>Etapa 1 Configurar Olá chave KMS adequada cliente instalação (para Windows Server 2016 e Windows Server 2012 R2)

Para Olá VM é criada a partir de uma imagem personalizada do Windows Server 2016 ou Windows Server 2012 R2, você deve configurar Olá chave KMS adequada cliente instalação para Olá VM.

Essa etapa não se aplica tooWindows 2012 ou Windows 2008 R2. Ele usa o recurso de ativação de máquina Virtual de automação (AVMA) hello, que é suportado apenas pelo Windows Server 2016 e Windows Server 2012 R2.

1. Execute **slmgr.vbs /dlv** em um prompt de comando elevado. Verifique Olá valor descrição na saída de hello e, em seguida, determine se ele foi criado de varejo (canal de varejo) ou mídia de licença de volume (VOLUME_KMSCLIENT):
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Se **slmgr.vbs /dlv** mostra o canal de varejo, executar Olá Olá de tooset comandos a seguir [chave de instalação de cliente KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) para a versão de saudação do Windows Server que está sendo usado e forçá-lo tooretry ativação: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Por exemplo, para Windows Server 2016 Datacenter, você executaria Olá comando a seguir:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>Verifique a etapa 2 Olá conectividade entre Olá VM e o serviço KMS do Azure

1. Baixe e extraia Olá [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) pasta local do tooa ferramenta no hello VM não ativa. 

2. Vá tooStart, pesquisar no Windows PowerShell, com o botão direito do Windows PowerShell e, em seguida, selecione Executar como administrador.

3. Certifique-se de que Olá que VM é configurada toouse Olá correto KMS do Azure do servidor. toodo isso, execute o seguinte comando:
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    Olá comando deve retornar: nome de máquina do serviço de gerenciamento de chaves definido tookms.core.windows.net:1688 com êxito.

4. Verificar usando Psping que você tenha conectividade toohello KMS servidor. Alternar toohello pasta onde você extraiu o download de Pstools.zip hello e, em seguida, execute o seguinte de saudação:
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  Na linha do segundo ao último Olá da saída de hello, certifique-se de que você vê: enviados = 4, recebidos = 4, perdidos = 0 (0% de perda).

  Se perdidos for maior que 0 (zero), Olá VM não tem servidor do KMS toohello conectividade. Nessa situação, se hello VM estiver em uma rede virtual e tiver um servidor DNS personalizado especificado, você deve verificar se esse servidor DNS é capaz de tooresolve kms.core.windows.net. Ou então, alterar Olá DNS server tooone que resolver kms.core.windows.net.

  Observe que, se você remover todos os servidores DNS de uma rede virtual, as VMs usam o serviço DNS interno do Azure. Esse serviço pode resolver kms.core.windows.net.
  
Também verifique se o que firewall Olá convidado não foi configurado de forma que impediriam a tentativas de ativação.

5. Depois de verificar tookms.core.windows.net conectividade bem-sucedida, execute Olá comando solicitados com privilégios elevados do Windows PowerShell a seguir. Esse comando tenta a ativação várias vezes.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

Uma ativação bem-sucedida retorna informações semelhantes a seguir hello:

**Ativando o Windows(R), edição ServerDatacenter (12345678-1234-1234-1234-12345678)... Produto ativado com sucesso.**

## <a name="faq"></a>Perguntas frequentes 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>Criei Olá Windows Server 2016 do Azure Marketplace. É necessário tooconfigure chave do KMS para ativação Olá Windows Server 2016? 
 
Não. imagem de saudação no Azure Marketplace tem Olá chave KMS adequada cliente instalação já configurado. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Trabalho de ativação do Windows hello mesmo maneira independentemente se Olá VM estiver usando o Azure híbrido Use benefício (HUB) ou não? 
 
Sim. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>O que acontece se o período de ativação do Windows expirar? 
 
Quando o período de cortesia de saudação expirou e o Windows ainda não está ativado, Windows Server 2008 R2 e versões posteriores do Windows mostrará notificações adicionais sobre a ativação. papel de parede da área de trabalho Olá permanece preto e Windows Update instalará a segurança e apenas atualizações críticas, mas as atualizações não opcionais. Olá notificações seção final Olá Olá [condições de licenciamento](http://technet.microsoft.com/en-us/library/ff793403.aspx) página.   

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
