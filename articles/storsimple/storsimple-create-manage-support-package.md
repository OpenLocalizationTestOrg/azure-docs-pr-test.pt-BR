---
title: aaaCreate um pacote de suporte do StorSimple | Microsoft Docs
description: Saiba como toocreate, descriptografar e editar um pacote de suporte para seu dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>Criar e gerenciar um pacote de suporte do StorSimple
## <a name="overview"></a>Visão geral
Um pacote de suporte do StorSimple é um mecanismo fácil de usar que coleta todos os logs relevantes tooassist Microsoft Support na solução de problemas no dispositivo StorSimple. Olá logs coletados são criptografados e compactados.

Este tutorial inclui instruções passo a passo toocreate e gerenciar o pacote de suporte de saudação.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Criar e carregar um pacote de suporte em Olá portal clássico do Azure
Você pode criar e carregar um site do Microsoft Support suporte pacote toohello por meio de saudação **manutenção** página serviço de saudação do hello portal clássico do Azure.

> [!NOTE]
> carregamento de saudação requer uma chave de acesso de suporte. Seu engenheiro de suporte deve fornecer esse tooyou em um email.
> 
> 

Um pacote de suporte criptografado e compactado (arquivo. cab) é criado e carregado toohello site de suporte. engenheiro de suporte de saudação pode então recuperar esse pacote hello no site de suporte para solução de problema de saudação.

Execute Olá etapas toocreate portal clássico Olá um pacote de suporte.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate um pacote de suporte em Olá portal clássico do Azure
1. Selecione **Dispositivos** > **Manutenção**.
2. Em Olá **pacote de suporte** seção, selecione **criar e carregar pacote de suporte**.
3. Em Olá **criar e carregar pacote de suporte** caixa de diálogo caixa, Olá a seguir:
   
    ![Criar um pacote de suporte](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * Em Olá **chave de acesso de suporte** texto, digite a chave de acesso de saudação. Seu engenheiro de suporte da Microsoft deve enviar tooyou esta chave de acesso no email.
   * Selecione Olá caixa de seleção tooprovide consentimento tooautomatically carregamento Olá suporte pacote toohello Microsoft Support site.
   * Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>Criar um pacote de suporte manualmente
Em alguns casos, você precisará toomanually criar pacote de suporte de saudação por meio do Windows PowerShell para StorSimple. Por exemplo:

* Se você precisar de informações confidenciais de tooremove de seu log de arquivos toosharing anterior com o Microsoft Support.
* Se você estiver tendo dificuldades para carregar o pacote hello devido a problemas de tooconnectivity.

Você pode compartilhar seu pacote de suporte gerado manualmente com o Suporte da Microsoft por email. Execute Olá seguindo as etapas toocreate um pacote de suporte no Windows PowerShell para StorSimple.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate um pacote de suporte no Windows PowerShell para StorSimple
1. toostart uma sessão do Windows PowerShell como administrador no computador remoto de saudação que tenha usado o dispositivo StorSimple tooyour tooconnect, digite Olá comando a seguir:
   
    `Start PowerShell`
2. Na sessão do Windows PowerShell hello, conecte-se toohello SSAdmin Console do seu dispositivo:
   
   * No prompt de comando hello, digite:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * Na caixa de diálogo de saudação que é aberta, digite sua senha de administrador do dispositivo. saudação padrão senha é:
     
      `Password1`
     
      ![Caixa de diálogo da credencial do PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * Selecione **OK**.
   * No prompt de comando hello, digite:
     
      `Enter-PSSession $MS`
3. Na sessão de saudação que é aberta, insira o comando apropriado hello.
   
   * Para compartilhamentos de rede protegidos por senha, insira:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Você será solicitado para uma senha, uma caminho toohello pasta compartilhada e uma senha de criptografia (porque o pacote de suporte de saudação é criptografado). Um pacote de suporte é criado na pasta especificada hello.
   * Para ações que não são protegidas por senha, você não precisa Olá `-Credential` parâmetro. Digite hello seguinte:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       pacote de suporte de saudação é criado para ambos os controladores na pasta compartilhada de rede especificado hello. É um arquivo criptografado e compactado que pode ser enviado tooMicrosoft suporte para solução de problemas. Para obter mais informações, consulte [Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>Olá parâmetros do cmdlet Export-HcsSupportPackage
Você pode usar o hello parâmetros com hello Export-HcsSupportPackage cmdlet a seguir.

| Parâmetro | Obrigatório/Opcional | Descrição |
| --- | --- | --- |
| `-Path` |Obrigatório |Use tooprovide Olá local da pasta compartilhada da rede Olá quais Olá pacote de suporte é colocado. |
| `-EncryptionPassphrase` |Obrigatório |Use tooprovide toohelp uma frase secreta criptografar o pacote de suporte de saudação. |
| `-Credential` |Opcional |Use credenciais de acesso de toosupply para a pasta compartilhada de rede hello. |
| `-Force` |Opcional |Use a etapa de confirmação de senha de criptografia do tooskip hello. |
| `-PackageTag` |Opcional |Usar toospecify um diretório em *caminho* que dão suporte a saudação pacote é colocado. padrão de saudação é [nome do dispositivo]-[data atual e a data]. |
| `-Scope` |Opcional |Especificar como **Cluster** toocreate (padrão) um pacote de suporte para ambos os controladores. Se você quiser toocreate um pacote somente para o controlador atual hello, especifique **controlador**. |

## <a name="edit-a-support-package"></a>Editar um pacote de suporte
Após gerar um pacote de suporte, talvez seja necessário tooedit Olá pacote tooremove sigilosos. Isso pode incluir nomes de volume, endereços IP do dispositivo e nomes de backup de arquivos de log de saudação.

> [!IMPORTANT]
> Você só pode editar um pacote de suporte que tenha sido gerado por meio do Windows PowerShell para StorSimple. Você não pode editar um pacote criado no hello portal clássico do Azure com o serviço StorSimple Manager.
> 
> 

tooedit um pacote de suporte antes de carregá-lo no site do Microsoft Support hello, primeiro descriptografar o pacote de suporte de hello, editar arquivos hello e, em seguida, criptografe-a novamente. Execute Olá etapas a seguir.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit um pacote de suporte no Windows PowerShell para StorSimple
1. Gerar um pacote de suporte, conforme descrito anteriormente, [toocreate um pacote de suporte no Windows PowerShell para StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Baixe o script hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente no seu cliente.
3. Importe o módulo do Windows PowerShell de saudação. Especifique Olá caminho toohello pasta local em que você baixou o script hello. módulo de saudação tooimport, digite:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Todos os arquivos de saudação são *. AES* arquivos que são compactados e criptografados. toodecompress e descriptografar arquivos, digite:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Observe que as extensões de arquivo real Olá agora são exibidas para todos os arquivos de saudação.
   
    ![Editar pacote de suporte](./media/storsimple-create-manage-support-package/IC750706.png)
5. Quando você for solicitado para a senha de criptografia hello, insira a frase secreta de saudação que você usou quando o pacote de suporte de saudação foi criado.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Procure pasta toohello que contém os arquivos de log hello. Porque os arquivos de log de Olá agora são descomprimidos e descriptografados, eles terão as extensões de arquivo original. Modificar esses arquivos tooremove todas as informações específicas do cliente, como nomes de volume e endereços IP do dispositivo e salvar arquivos hello.
7. Olá fechar arquivos toocompress-los com gzip e criptografá-los com AES-256. Isso é para velocidade e segurança durante a transferência de pacote de suporte de saudação em uma rede. toocompress e criptografar os arquivos, digite Olá seguinte:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Editar pacote de suporte](./media/storsimple-create-manage-support-package/IC750707.png)
8. Quando solicitado, forneça uma senha de criptografia para o pacote de suporte modificado hello.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Anote Olá nova senha, para que você pode compartilhá-lo com o Microsoft Support quando solicitado.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Exemplo: edição de arquivos em um pacote de suporte em um compartilhamento protegido por senha
saudação de exemplo a seguir mostra como toodecrypt, editar e criptografar novamente um pacote de suporte.

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[use pacotes de suporte e dispositivo logs tootroubleshoot sua implantação de dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

