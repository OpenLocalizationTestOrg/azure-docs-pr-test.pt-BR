---
title: aaaPrepare tooAzure de tooupload um VHD do Windows | Microsoft Docs
description: Como um VHD do Windows ou o VHDX tooprepare antes de carregar tooAzure
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Preparar um tooAzure de tooupload Windows VHD ou VHDX
Antes de carregar um máquinas virtuais do Windows (VM) do local tooMicrosoft do Azure, você deve preparar saudação do disco rígido virtual (VHD ou VHDX). O Azure suporta apenas máquinas virtuais de geração 1 no formato de arquivo VHD hello e têm um disco de tamanho fixo. tamanho máximo de saudação permitido para Olá que VHD é 1.023 GB. Você pode converter uma geração 1 VM da saudação VHDX tooVHD do sistema de arquivos e de uma expansão dinâmica toofixed tamanho de disco. No entanto, não é possível alterar a geração de uma VM. Para obter mais informações, consulte [Devo criar uma VM de geração 1 ou 2 no Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).

Para obter mais informações sobre a política de suporte de saudação VM do Azure, consulte [suporte de software de servidor da Microsoft para máquinas virtuais do Microsoft Azure](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> instruções de saudação neste artigo se aplicam a toohello versão de 64 bits do Windows Server 2008 R2 e posterior sistema operacional Windows. Para obter informações sobre como executar a versão de 32 bits do sistema operacional no Azure, consulte [Suporte para sistemas operacionais de 32 bits em máquinas virtuais do Azure](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Converter Olá tooVHD de disco virtual e disco de tamanho fixo 
Se você precisar tooconvert toohello seu disco virtual necessário formato do Azure, use um dos métodos de saudação nesta seção. Faça backup Olá VM antes de executar o processo de conversão do disco virtual hello e certifique-se de que Olá que VHD do Windows funciona corretamente no servidor de local de saudação. Resolva quaisquer erros no hello própria máquina virtual antes de você tentar tooconvert ou carregá-lo tooAzure.

Depois de converter disco hello, crie uma VM que usa o disco Olá convertido. Iniciar e entrar em toohello VM toofinish Preparando Olá VM para carregamento.

### <a name="convert-disk-using-hyper-v-manager"></a>Converter disco usando o Gerenciador do Hyper-V
1. Abra o Gerenciador do Hyper-V e selecione o computador local Olá esquerda. No menu de saudação acima da lista de saudação do computador, clique em **ação** > **Editar disco**.
2. Em Olá **localizar disco rígido Virtual** tela, localize e selecione o disco virtual.
3. Em Olá **escolher ação** tela e, em seguida, selecione **converter** e **próximo**.
4. Se você precisar tooconvert vhdx, selecione **VHD** e, em seguida, clique em **Avançar**
5. Se você precisar tooconvert de um disco de expansão dinâmica, selecione **tamanho fixo** e, em seguida, clique em **Avançar**
6. Localize e selecione um caminho toosave Olá novo arquivo VHD.
7. Clique em **Concluir**.

>[!NOTE]
>comandos Olá neste artigo devem ser executados em uma sessão do PowerShell com privilégios elevados.

### <a name="convert-disk-by-using-powershell"></a>Converter disco usando o PowerShell
Você pode converter um disco virtual usando Olá [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) comando no Windows PowerShell. Escolha **Executar como administrador** ao iniciar o PowerShell. 

Olá comando de exemplo a seguir converte de VHDX tooVHD e de um expansão dinâmica toofixed-tamanho do disco:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
Neste comando, substitua o valor de saudação de "-Path" com hello caminho toohello disco rígido virtual que você deseja tooconvert e hello valor para "-DestinationPath" com hello novo caminho e nome de saudação convertido em disco.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Converter do formato de disco VMware VMDK
Se você tiver uma imagem de VM do Windows em Olá [formato de arquivo VMDK](https://en.wikipedia.org/wiki/VMDK), converta-tooa VHD usando Olá [conversor de VM do Microsoft](https://www.microsoft.com/download/details.aspx?id=42497). Para obter mais informações, consulte o artigo de blog Olá [como tooConvert um VHD do VMware VMDK V tooHyper](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Definir configurações do Windows para o Azure

Em Olá VM que você planejar tooupload tooAzure, execute todos os comandos seguintes Olá etapas de um [janela de Prompt de comando com privilégios elevados](https://technet.microsoft.com/library/cc947813.aspx):

1. Remova qualquer rota estática persistente na tabela de roteamento hello:
   
   * tabela de rota Olá tooview, execute `route print` no prompt de comando hello.
   * Verificar Olá **rotas de persistência** seções. Se houver uma rota persistente, use [excluir rota](https://technet.microsoft.com/library/cc739598.apx) tooremove-lo.
2. Remova do proxy WinHTTP hello:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Definir a política de SAN de disco de saudação muito[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    Na janela de Prompt de comando aberta hello, digite Olá comandos a seguir:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Definir o Horário Coordenado Universal (UTC) para Windows e Olá muito o tipo de inicialização de serviço de tempo do Windows (w32time) do hello**automaticamente**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Definir toohello de perfil de energia Olá **alto desempenho**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Verifique os serviços do Windows hello
Certifique-se de que cada Olá serviços do Windows a seguir é definida toohello **valores padrão do Windows**. Esses são números de mínimo de saudação de serviços que devem ser configurados toomake-se de que Olá VM tem conectividade. configurações de inicialização em Olá tooreset, executadas Olá comandos a seguir:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Atualizar configurações de registro da Área de Trabalho Remota
Certifique-se de que Olá configurações a seguir estão configurados corretamente para conexão de área de trabalho remota:

>[!Note] 
>Você receberá uma mensagem de erro quando você executa Olá **Set-ItemProperty-Path ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal serviços - nome &lt;nome do objeto&gt; &lt;valor&gt;** nessas etapas. mensagem de saudação do erro pode ser ignorada. Isso significa que somente esse domínio Olá não está fazendo com que a configuração por meio de um objeto de diretiva de grupo.
>
>

1. O protocolo RDP está habilitado:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Olá porta RDP está configurado corretamente (porta 3389 padrão):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Quando você implantar uma VM, as regras padrão Olá são criadas em relação a porta 3389. Se desejar que o número da porta toochange hello, faça-o após Olá VM é implantada no Azure.

3. Olá ouvinte está escutando em cada interface de rede:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Configure o modo de autenticação no nível da rede Olá para conexões de RDP hello:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Definir valor keep-alive hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Reconecte:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Limitar o número de conexões simultâneas hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. Se houver que quaisquer certificados autoassinados vinculado toohello ouvinte RDP, removê-los:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Isso é toomake-se de que você pode conectar o início de hello quando você implanta Olá VM. Você também pode analisar isso em um estágio posterior após Olá que VM é implantada no Azure, se necessário.

9. Se Olá VM será parte de um domínio, verifique todos Olá seguir configurações toomake-se de que as configurações de anterior de saudação não são revertidas. Olá políticas devem ser verificadas são seguinte hello:
    
    - O RDP está habilitado:

         Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:
         
         **Permitir que os usuários tooconnect remotamente usando a área de trabalho remota**

    - Política de grupo do NLA:

        Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security: 
        
        **Exigir a Autenticação de usuário para conexões remotas usando a Autenticação no Nível da Rede**
    
    - Configurações de Keep Alive:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **Configurar o intervalo de conexão keep alive**

    - Configurações de reconexão:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **Reconexão automática**

    - Limitar o número de saudação de configurações de conexões:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **Limitar o número de conexões**

## <a name="configure-windows-firewall-rules"></a>Configure as regras do Firewall do Windows
1. Ative Firewall do Windows em perfis de saudação três (domínio, padrão e público):

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Execute Olá a seguir de comando do PowerShell tooallow WinRM através dos perfis de firewall Olá três (domínio, privado e público) e habilitar Olá serviço remoto do PowerShell:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Habilitar Olá seguindo o tráfego de RDP da saudação de tooallow de regras de firewall 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Habilite a regra de compartilhamento de impressora e Olá arquivo para que hello VM pode responder tooa comando de ping dentro Olá rede Virtual:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Se Olá VM será parte de um domínio, verifique Olá seguir configurações toomake-se de que as configurações de anterior de saudação não são revertidas. políticas de saudação AD que devem ser verificadas são seguinte hello:

    - Habilitar perfis de Firewall do Windows hello

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Proteger todas as conexões de rede**

       Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Proteger todas as conexões de rede**

    - Habilitar o RDP 

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Permitir exceções de entrada da Área de Trabalho Remota**

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Permitir exceções de entrada da Área de Trabalho Remota**

    - Habilitar o ICMP-V4

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Permitir exceções do ICMP**

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Permitir exceções do ICMP**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Verifique se a VM está em estado íntegro, segura e pode ser acessada com RDP 
1. disco de saudação se toomake está íntegro e consistente, execute uma operação de verificação de disco na próxima reinicialização VM hello:

    ```PowerShell
    Chkdsk /f
    ```
    Certifique-se de que o relatório de saudação mostra um disco íntegro e limpo.

2. Defina configurações de dados de configuração da inicialização (BCD) hello. 

    > [!Note]
    > Certifique-se de executar esses comandos em uma janela CMD elevada e **não** no PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Verifique se que esse repositório desse serviço de gerenciamento do Windows instrumentação Olá é consistente. tooperform, Olá executar comando a seguir:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Se o repositório de saudação estiver corrompido, consulte [WMI: o repositório está corrompido, ou não](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Certifique-se de que qualquer outro aplicativo não está usando a porta 3389 hello. Esta porta é usada para Olá serviço RDP no Azure. Você pode executar **netstat - anob** toosee quais portas estão em usadas em Olá VM:

    ```PowerShell
    netstat -anob
    ```

5. Se Olá VHD do Windows que você deseja tooupload for um controlador de domínio, siga estas etapas:

    R. Execute [estas etapas adicionais](https://support.microsoft.com/kb/2904015) tooprepare disco de saudação.

    B. Certifique-se de que você sabe a senha do DSRM Olá caso você tenha toostart Olá VM no DSRM em algum momento. Talvez você queira toorefer toothis link Olá tooset [senha DSRM](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Verifique se a senha e a conta de administrador interno Olá são conhecidos tooyou. Você pode deseja senha de administrador local atual do tooreset hello e certifique-se de que você pode usar essa conta toosign em tooWindows por meio de saudação conexão RDP. Essa permissão de acesso é controlado pelo objeto de diretiva de grupo "Permitir logon pelos serviços de área de trabalho remota" hello. Você pode exibir esse objeto no Editor de diretiva de Grupo Local de saudação em:

    Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment

7. Saudação de seleção a seguir AD políticas toomake-se de que você não está bloqueando o acesso RDP via RDP nem de rede hello:

    - Configuration\Windows Settings\Security Settings\Local políticas direitos Assignment\Deny acesso toothis computador da rede Olá

    - Configuração do Computador\Configurações do Windows\Configurações de Segurança\Políticas Locais\Atribuição de direitos de usuário\Negar logon pelos Serviços de Área de Trabalho Remota


8. Reinicialização Olá VM toomake-se de que o Windows está íntegro ainda pode ser alcançado usando a conexão de RDP hello. Neste ponto, você pode desejar toocreate uma máquina virtual em seu local Hyper-V toomake se Olá que VM está iniciando completamente e, em seguida, testar se é acessível de RDP.

9. Remova os filtros extras da Interface do Driver de Transporte, como software que analisa pacotes TCP ou firewalls extras. Você também pode analisar isso em um estágio posterior após Olá que VM é implantada no Azure, se necessário.

10. Desinstale qualquer software de terceiros e driver componentes relacionados toophysical ou qualquer outra tecnologia de virtualização.

### <a name="install-windows-updates"></a>Instalar atualizações do Windows
configuração ideal Olá é muito**ter nível de patch de saudação da máquina de saudação em hello mais recente**. Se isso não for possível, certifique-se de que Olá atualizações a seguir estão instalados:

|                       |                   |           |                                       Versão mínima do arquivo x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Componente               | Binário            | Windows 7 e Windows Server 2008 R2 | Windows 8 e Windows Server 2012             | Windows 8.1 e Windows Server 2012 R2 | Windows 10 e Windows Server 2016 RS1 | Windows 10 RS2             |
| Armazenamento                 | disk.sys          | 6.1.7601.23403 – KB3125574         | 6.2.9200.17638/6.2.9200.21757 – KB3137061 | 6.3.9600.18203 – KB3137061           | -                                    | -                          |
|                         | storport.sys      | 6.1.7601.23403 – KB3125574         | 6.2.9200.17188/6.2.9200.21306 – KB3018489 | 6.3.9600.18573 – KB4022726           | 10.0.14393.1358 – KB4022715          | 10.0.15063.332             |
|                         | ntfs.sys          | 6.1.7601.23403 – KB3125574         | 6.2.9200.17623/6.2.9200.21743 – KB3121255 | 6.3.9600.18654 – KB4022726           | 10.0.14393.1198 – KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 – KB3125574         | 6.2.9200.16384 – KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 – KB3125574         | 6.2.9200.17061/6.2.9200.21180 – KB2995387 | 6.3.9600.18334 – KB3172614           | 10.0.14393.953 – KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 – KB3125574         | 6.2.9200.17047/6.2.9200.21165 – KB2975331 | 6.3.9600.18265 – KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 – KB3125574         | 6.2.9200.16681 – KB2877114                  | 6.3.9600.17401 – KB3000850           | 10.0.14393.953 – KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 – KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 – KB3125574         | 6.2.9200.21006 – KB2955163                  | 6.3.9600.18624 – KB4022726           | 10.0.14393.1066 – KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 – KB3125574         | 6.2.9200.21474 – KB3046101                  | 6.3.9600.18592 – KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 – KB3125574         | 6.2.9200.21190 – KB3046101                  | 6.3.9600.18616 – KB4022726           | 10.0.14393.1198 – KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 – KB3125574         | 6.2.9200.20930 – KB2930244                  | 6.3.9600.18294 – KB3172614           | 10.0.14393.576 – KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 – KB3125574         | 6.2.9200.20930 – KB2930244                  | 6.3.9600.17415 – KB3172614           | 10.0.14393.206 – KB4022715           | -                          |
| Rede                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 – KB4022715          | 10.0.15063.250 – KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 – KB4022722         | 6.2.9200.22108 – KB4022724                  | 6.3.9600.18603 – KB4022726           | 10.0.14393.479 – KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 – KB4022722         | 6.2.9200.21548 – KB4022724                  | 6.3.9600.18586 – KB4022726           | 10.0.14393.953 – KB4022715           | 10.0.15063.483             |
|                         | mrxsmb.sys        | 6.1.7601.23816 – KB4022722         | 6.2.9200.22074 – KB4022724                  | 6.3.9600.18586 – KB4022726           | 10.0.14393.953 – KB4022715           | 10.0.15063.0               |
|                         | tcpip.sys         | 6.1.7601.23761 – KB4022722         | 6.2.9200.22070 – KB4022724                  | 6.3.9600.18478 – KB4022726           | 10.0.14393.1358 – KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 – KB3125574         | 6.2.9200.17285 – KB3042553                  | 6.3.9600.18574 – KB4022726           | 10.0.14393.251 – KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 – KB4022719         | 6.2.9200.22117 – KB4022724                  | 6.3.9600.18654 – KB4022726           | 10.0.14393.1358 – KB4022715          | 10.0.15063.138             |
| Núcleo                    | ntoskrnl.exe      | 6.1.7601.23807 – KB4022719         | 6.2.9200.22170 – KB4022718                  | 6.3.9600.18696 – KB4022726           | 10.0.14393.1358 – KB4022715          | 10.0.15063.483             |
| Serviços da Área de Trabalho Remota | rdpcorets.dll     | 6.2.9200.21506 – KB4022719         | 6.2.9200.22104 – KB4022724                  | 6.3.9600.18619 – KB4022726           | 10.0.14393.1198 – KB4022715          | 10.0.15063.0               |
|                         | termsrv.dll       | 6.1.7601.23403 – KB3125574         | 6.2.9200.17048 – KB2973501                  | 6.3.9600.17415 – KB3000850           | 10.0.14393.0 – KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 – KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | win32k.sys        | 6.1.7601.23807 – KB4022719         | 6.2.9200.22168 – KB4022718                  | 6.3.9600.18698 – KB4022726           | 10.0.14393.594 – KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 – KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | rdpwd.sys         | 6.1.7601.23403 – KB3125574         | -                                           | -                                    | -                                    | -                          |
| Segurança                | Vencimento tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Quando o sysprep toouse<a id="step23"></a>    

O Sysprep é um processo que você pode executar em uma instalação do windows que redefinirá a instalação de saudação do sistema hello e fornecerá um "hello configuração inicial pelo usuário" removendo todos os dados pessoais e redefinindo vários componentes. Você normalmente faz isso se você quiser toocreate um modelo do qual você pode implantar várias outras VMs que têm uma configuração específica. Isso é chamado de uma **imagem generalizada**.

Se, em vez disso, você deseja toocreate apenas uma máquina virtual de um disco, você não tem toouse sysprep. Nessa situação, você pode apenas criar hello VM a partir do qual é conhecido como um **imagem especializada**.

Para obter mais informações sobre como toocreate uma VM em um disco especializado, consulte:

- [Criar uma VM com base em um disco especializado](create-vm-specialized.md)
- [Criar uma VM com base em um disco VHD](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Se você quiser toocreate uma imagem generalizada, é necessário toorun sysprep. Para obter mais informações sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx). 

Nem toda função ou aplicativo que é instalado em um computador baseado no Windows dá suporte a essa generalização. Portanto, antes de você executar esse procedimento, consulte toohello toomake do artigo a seguir se essa função de saudação do computador é compatível com o sysprep. Para obter mais informações, consulte [Suporte do Sysprep em funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

### <a name="steps-toogeneralize-a-vhd"></a>Etapas toogeneralize um VHD

>[!NOTE]
> Depois de executar o sysprep.exe como Olá especificado nas etapas a seguir, desligue Olá VM e não ativá-lo novamente até que você crie uma imagem no Azure.

1. Entrar toohello VM do Windows.
2. Execute o **Prompt de Comando** como administrador. 
3. Altere o diretório para hello: **%windir%\system32\sysprep**e, em seguida, execute **sysprep.exe**.
3. Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que Olá **generalizar** caixa de seleção é marcada.

    ![Ferramenta de Preparação do Sistema](media/prepare-for-upload-vhd-image/syspre.png)
4. Em **Opções de Desligamento**, selecione **Desligar**.
5. Clique em **OK**.
6. Quando o Sysprep for concluído, desligue Olá VM. Não use **reiniciar** tooshut para baixo Olá VM.
7. Agora hello VHD está pronto toobe carregado. Para obter mais informações sobre como toocreate uma VM em um disco generalizado, consulte [carregar um VHD generalizado e usá-lo toocreate um novas VMs no Azure](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Conclua as configurações recomendadas
Olá configurações a seguir não afeta o VHD upload. No entanto, é altamente recomendável que você as configure.

* Instalar Olá [agente de VMs do Azure](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Em seguida, você pode habilitar as extensões de VM. extensões de VM Olá implementam a maioria das funcionalidades essenciais de saudação que você pode desejar toouse com suas VMs, como a redefinição de senhas, configuração de RDP e assim por diante. Para obter mais informações, consulte:

    - [Agente de VM e extensões – parte 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [Agente de VM e extensões – parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* log de despejo Olá pode ser útil para solucionar problemas de falha do Windows. Habilite coleta de log de despejo hello:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Se você receber erros em qualquer um dos procedimentos de saudação as etapas neste artigo, isso significa que as chaves do registro de saudação já existe. Nessa situação, use Olá comandos a seguir em vez disso:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Depois Olá VM é criada no Azure, recomendamos que você coloque o arquivo de paginação de saudação em desempenho de tooimprove hello "Unidade de tempo" volume. Configure isso da seguinte maneira:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Se houver qualquer disco de dados que é anexado toohello VM, a letra da unidade do volume da unidade Temporal Olá costuma ser "D." Essa designação pode ser diferente, dependendo do número de saudação de unidades disponíveis e as configurações de saudação feitas.

## <a name="next-steps"></a>Próximas etapas
* [Carregar um tooAzure de imagem de VM do Windows para implantações do Gerenciador de recursos](upload-generalized-managed.md)

