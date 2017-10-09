---
title: "problemas de implantação StorSimple aaaTroubleshoot | Microsoft Docs"
description: "Descreve como toodiagnose e corrigir erros que ocorrem quando você implanta StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>Solucionar problemas de implantação do dispositivo StorSimple
## <a name="overview"></a>Visão geral
Este artigo oferece orientações úteis de solução de problemas para sua implantação do Microsoft Azure StorSimple. Descreve problemas comuns, possíveis causas e etapas recomendadas toohelp que resolver problemas que podem ocorrer quando você configura o StorSimple. Essas informações se aplicam a dispositivo físico tooboth Olá StorSimple local e o dispositivo virtual StorSimple hello.

> [!NOTE]
> Problemas relacionados à configuração de dispositivo que você pode enfrentar podem ocorrer quando você implanta dispositivo Olá Olá primeira vez, ou eles podem ocorrer posteriormente, quando o dispositivo hello está operacional. Este artigo se concentra na solução de problemas da primeira implantação. tootroubleshoot um dispositivo operacional, ir muito[solucionar problemas de dispositivo operacional](storsimple-troubleshoot-operational-device.md).
> 
> 

Este artigo também descreve as ferramentas de saudação para implantações de StorSimple de solução de problemas e fornece um exemplo passo a passo de solução de problemas.

## <a name="first-time-deployment-issues"></a>Problemas da primeira implantação
Se você tiver um problema ao implantar seu dispositivo para Olá primeira vez, considere o seguinte hello:

* Se você estiver solucionando problemas de um dispositivo físico, certifique-se de que hardware Olá foi instalado e configurado conforme descrito em [instalar seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) ou [instalar seu dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
* Verifique os pré-requisitos da implantação. Certifique-se de que você tenha todas as informações de saudação descritas em Olá [lista de verificação de configuração de implantação](storsimple-deployment-walkthrough.md#deployment-configuration-checklist).
* Examine Olá notas de versão do StorSimple toosee se Olá problema é descrito. Notas de versão de Hello incluem soluções alternativas para problemas de instalação conhecidos. 

Durante a implantação de dispositivo, a saudação mais comuns problemas que os usuários enfrentam ocorrem quando executarem o Assistente de instalação de saudação e quando eles registrar dispositivo Olá através do Windows PowerShell para StorSimple. (Você usa o Windows PowerShell para StorSimple tooregister e configurar seu dispositivo StorSimple. Para obter mais informações sobre o registro de dispositivos, consulte [Etapa 3: configurar e registrar seu dispositivo por meio do Windows PowerShell para StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

Olá seções a seguir pode ajudá-lo a resolver problemas encontrados ao configurar o dispositivo StorSimple Olá Olá primeira vez.

## <a name="first-time-setup-wizard-process"></a>Processo do assistente de instalação inicial
Olá etapas a seguir resumem o processo do Assistente de instalação de saudação. Para obter informações detalhadas sobre instalação, consulte [Implantar o dispositivo StorSimple local](storsimple-deployment-walkthrough.md).

1. Executar Olá [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) cmdlet toostart Olá Assistente de instalação que orientará você durante saudação restantes etapas. 
2. Configurar rede Olá: Assistente de instalação Olá lhe permite configurar as configurações de rede para interface de rede 0 Olá dados em seu dispositivo StorSimple. Essas configurações incluem o seguinte hello:
   * Olá virtual IP (VIP), máscara de sub-rede e gateway – [Set-HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) cmdlet é executado no plano de fundo de saudação. Ele configura o endereço IP hello, máscara de sub-rede e gateway Olá dados 0 interface de rede no seu dispositivo StorSimple.
   * Servidor DNS primário – Olá [Set-HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) cmdlet é executado no plano de fundo de saudação. Ele configura as configurações de DNS Olá para sua solução StorSimple.
   * O servidor NTP – Olá [Set-HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet é executado no plano de fundo de saudação. Ele configura as configurações do servidor NTP Olá para sua solução StorSimple.
   * Opcional proxy da web – hello [Set-HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) cmdlet é executado no plano de fundo de saudação. Ele define e permite a configuração do proxy web Olá para sua solução StorSimple.
3. Configurar senhas de saudação: Olá próxima etapa é tooset o administrador do dispositivo e senhas do Gerenciador de instantâneos do StorSimple. Se você estiver executando a atualização 1, em seguida, não será necessário tooset a senha do StorSimple Snapshot Manager hello.
   
   * senha de administrador de dispositivo de saudação é toolog usado no dispositivo tooyour. senha do dispositivo padrão Olá é **Password1**.
   * senha do StorSimple Snapshot Manager Olá é necessária quando você configura um toouse dispositivo StorSimple Snapshot Manager. Você precisa toofirst conjunto Olá senha no Assistente de instalação de saudação e, em seguida, você pode definir e alterá-lo de saudação serviço StorSimple Manager. Essa senha autentica o dispositivo de saudação com o Gerenciador de instantâneos do StorSimple.
     
     > [!IMPORTANT]
     > Senhas são coletadas antes do registro, mas aplicadas somente depois que você registrar o dispositivo Olá com êxito. Se houver uma falha tooapply uma senha, você será toosupply solicitadas Olá senha novamente até Olá necessário senhas (que atendem aos requisitos de complexidade de saudação) sejam coletadas.
     > 
     > 
4. Registrar o dispositivo Olá: Olá última etapa é o dispositivo de saudação tooregister com o serviço StorSimple Manager Olá em execução no Microsoft Azure. Olá registro exige que você muito[obter chave de registro de serviço Olá](storsimple-manage-service.md#get-the-service-registration-key) de Olá portal clássico do Azure e fornecê-la no Assistente de instalação de saudação. Depois que o dispositivo Olá é registrado com êxito, uma chave de criptografia de dados de serviço é fornecida tooyou. Certifique-se de que tookeep essa criptografia chave em um local seguro, pois ela será necessária tooregister todos os dispositivos subsequentes com o serviço de saudação.

## <a name="common-errors-during-device-deployment"></a>Erros comuns durante a implantação de dispositivo
Olá seguintes tabelas lista Olá comuns erros que podem ocorrer quando você:

* Configurações de rede Olá necessário.
* Defina configurações de proxy web opcional hello.
* Configure o administrador do dispositivo hello e senhas do Gerenciador de instantâneos do StorSimple. 
* Dispositivo de saudação do registro. 

## <a name="errors-during-hello-required-network-settings"></a>Erros durante a saudação necessárias configurações de rede
| Não. | Mensagem de erro | Possíveis causas | Ação recomendada |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Este comando só pode ser executado no controlador ativo hello. |Configuração estava sendo executada no controlador passivo hello. |Execute este comando no controlador ativo hello. Para saber mais, consulte [Identificar um controlador ativo em seu dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard: o dispositivo não está pronto. |Há problemas de conectividade de rede Olá no DATA 0. |Verifique a conectividade de rede física Olá no DATA 0. |
| 3 |Invoke-HcsSetupWizard: Há um conflito de endereços IP com outro sistema na rede da saudação (exceção de HRESULT: 0x80070263). |Olá IP fornecido para DATA 0 já estava em uso por outro sistema. |Forneça um novo IP que não esteja em uso. |
| 4 |Invoke-HcsSetupWizard: falha em um recurso de cluster. (Exceção de HRESULT: 0x800713AE). |Duplique o VIP. IP Hello fornecido já está em uso. |Forneça um novo IP que não esteja em uso. |
| 5 |Invoke-HcsSetupWizard: endereço IPv4 inválido. |endereço IP de saudação é fornecido em um formato incorreto. |Verifique o formato de saudação e forneça o endereço IP novamente. Para saber mais, consulte [Endereçamento Ipv4][1]. |
| 6 |Invoke-HcsSetupWizard: endereço IPv6 inválido. |endereço IP de saudação é fornecido em um formato incorreto. |Verifique o formato de saudação e forneça o endereço IP novamente. Para saber mais, consulte [Endereçamento Ipv6][2]. |
| 7 |Invoke-HcsSetupWizard: não há mais nenhum ponto de extremidade disponíveis do mapeador de ponto de extremidade de saudação. (Exceção de HRESULT: 0x800706D9) |funcionalidade de saudação do cluster não está funcionando. |[Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para as próximas etapas. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Erros durante a saudação opcional de configurações de proxy da web
| Não. | Mensagem de erro | Possíveis causas | Ação recomendada |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: parâmetro inválido (exceção de HRESULT: 0x80070057) |Um dos parâmetros de saudação fornecidos para as configurações de proxy de saudação não é válido. |Olá URI não é fornecido no formato correto de saudação. Olá Use seguindo o formato: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: servidor RPC não disponível (exceção de HRESULT: 0x800706ba) |causas de saudação é Olá seguinte:<ol><li>Olá cluster não está ativo.</li><li>controlador passivo Olá não pode se comunicar com o controlador ativo hello e Olá comando é executado no controlador passivo.</li></ol> |Dependendo da causa hello:<ol><li>[Entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) toomake-se de que esse cluster hello está ativo.</li><li>Execute o comando de saudação do controlador ativo hello. Se desejar que o comando de saudação toorun no controlador passivo hello, você precisará tooensure esse controlador passivo Olá pode se comunicar com o controlador ativo hello. Você precisará de muito[entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) se essa conectividade estiver interrompida.</li></ol> |
| 3 |Invoke-HcsSetupWizard: falha na chamada RPC (exceção de HRESULT: 0x800706be) |O cluster está inoperante. |[Entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) toomake-se de que esse cluster hello está ativo. |
| 4 |Invoke-HcsSetupWizard: recurso de cluster não encontrado (exceção de HRESULT: 0x8007138f) |o recurso de cluster Olá não foi encontrado. Isso pode acontecer quando a instalação de saudação não estava correta. |Configurações de padrão de fábrica tooreset Olá dispositivo toohello talvez seja necessário. [Entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) toocreate um recurso de cluster. |
| 5 |Invoke-HcsSetupWizard: Cluster recurso não online (exceção de HRESULT: 0x8007138c) |Os recursos de cluster não estão online. |[Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para as próximas etapas. |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>Erros relacionados toodevice administrador e senhas do Gerenciador de instantâneos StorSimple
senha de administrador de dispositivo saudação padrão é **Password1**. Essa senha expira após o primeiro logon do hello; Portanto, você precisará toouse Olá instalação Assistente toochange-lo. Quando você registrar o dispositivo Olá Olá primeira vez, você deve fornecer uma nova senha de administrador do dispositivo. 

Se você usar o software do Gerenciador de instantâneos StorSimple Olá em execução no dispositivo de Olá Olá Windows Server host toomanage, também deve fornecer uma senha do StorSimple Snapshot Manager durante o registro pela primeira vez. 

Certifique-se de que suas senhas atendam Olá requisitos a seguir:

* Sua senha do administrador do dispositivo deve ter entre 8 e 15 caracteres.
* Sua senha do Gerenciador de Instantâneos StorSimple deve ter 14 ou 15 caracteres.
* As senhas devem conter 3 de saudação 4 tipos de caracteres a seguir: minúsculos, maiusculos, numéricos e especiais. 
* Sua senha não pode ser Olá mesmas Olá últimas 24 senhas.

Além disso, tenha em mente que as senhas expiram a cada ano e pode ser alterada somente depois que você registrar o dispositivo Olá com êxito. Se o registro de saudação falhar por algum motivo, Olá senhas não serão alteradas. Para obter mais informações sobre o administrador do dispositivo e senhas do StorSimple Snapshot Manager, vá muito[Use Olá toochange do serviço StorSimple Manager suas senhas StorSimple](storsimple-change-passwords.md).

Você pode encontrar um ou mais dos Olá os erros a seguir ao configurar o administrador do dispositivo hello e senhas do Gerenciador de instantâneos do StorSimple.

| Não. | Mensagem de erro | Ação recomendada |
| --- | --- | --- |
| 1 |senha de saudação excede o comprimento máximo de saudação. |Use uma senha que atenda a estes requisitos:<ul><li>A senha de administrador do dispositivo deve ter entre 8 e 15 caracteres.</li><li>A senha do StorSimple Snapshot Manager deve ter de 14 a 15 caracteres.</li></ul> |
| 2 |Olá senha não atende comprimento Olá necessário. |Use uma senha que atenda a estes requisitos:<ul><li>A senha de administrador do dispositivo deve ter entre 8 e 15 caracteres.</li><li>A senha do StorSimple Snapshot Manager deve ter de 14 a 15 caracteres.</lu></ul> |
| 3 |senha de saudação deve conter caracteres minúsculos. |As senhas devem conter 3 de saudação 4 tipos de caracteres a seguir: minúsculos, maiusculos, numéricos e especiais. Certifique-se de que sua senha atende a esses requisitos. |
| 4 |senha de saudação deve conter caracteres numéricos. |As senhas devem conter 3 de saudação 4 tipos de caracteres a seguir: minúsculos, maiusculos, numéricos e especiais. Certifique-se de que sua senha atende a esses requisitos. |
| 5 |senha de saudação deve conter caracteres especiais. |As senhas devem conter 3 de saudação 4 tipos de caracteres a seguir: minúsculos, maiusculos, numéricos e especiais. Certifique-se de que sua senha atende a esses requisitos. |
| 6 |Olá senha deve conter 3 de saudação seguintes 4 tipos de caracteres: letras maiusculas, letras minúsculas, numéricos e especiais. |Sua senha não contém tipos Olá necessário de caracteres. Certifique-se de que sua senha atende a esses requisitos. |
| 7 |O parâmetro não corresponde à confirmação. |Certifique-se de que sua senha atende a todos os requisitos e de que ela tenha sido inserida corretamente. |
| 8 |Sua senha não pode coincidir com o padrão de saudação. |a senha padrão Olá é *Password1*. É necessário toochange essa senha depois de fazer logon para Olá primeira vez. |
| 9 |senha Olá que você inseriu não corresponde senha de saudação do dispositivo. Digite novamente a senha de saudação. |Olá senha e digite-a novamente. |

As senhas são coletadas antes de dispositivo hello está registrado, mas são aplicadas apenas após o registro bem-sucedido. fluxo de trabalho de recuperação de senha Olá requer Olá dispositivo toobe registrado. 

> [!IMPORTANT]
> Em geral, se uma tentativa de tooapply uma senha falha, então software Olá tenta repetidamente a senha de saudação toocollect até obter êxito. Em casos raros, a senha de saudação não pode ser aplicada. Nessa situação, você pode registrar o dispositivo hello e continuar, porém as senhas de saudação não serão alteradas. Você não receberá nenhuma indicação como toowhich senha não foi alterada — senha de administrador do dispositivo hello ou senha do StorSimple Snapshot Manager hello. Se essa situação ocorrer, recomendamos que você altere as duas senhas.
> 
> 

Você pode redefinir senhas Olá Olá portal clássico do Azure por meio de saudação serviço StorSimple Manager. Para obter mais informações, consulte: 

* [Senha de administrador de dispositivo alteração Olá](storsimple-change-passwords.md#change-the-device-administrator-password).
* [Alterar senha do Gerenciador de instantâneos StorSimple de saudação](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

## <a name="errors-during-device-registration"></a>Erros durante o registro de dispositivo
Você usar o serviço StorSimple Manager Olá em execução no dispositivo do Microsoft Azure tooregister hello. Você pode encontrar um ou mais dos Olá seguintes problemas durante o registro do dispositivo.

| Não. | Mensagem de erro | Possíveis causas | Ação recomendada |
| --- | --- | --- | --- |
| 1 |Erro 350027: Falha tooregister dispositivo Olá Olá StorSimple Manager. | |Aguarde alguns minutos e tente novamente a operação de saudação. Se o problema de saudação persistir, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md). |
| 2 |Erro 350013: Ocorreu um erro ao registrar o dispositivo hello. Isso pode ser devido a chave de registro de serviço tooincorrect. | |Registre Olá dispositivo novamente com a chave de registro de serviço correta de saudação. Para obter mais informações, consulte [chave de registro de serviço Get hello.](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |Erro 350063: Autenticação tooStorSimple service Manager passado, mas falha no registro. Repita a operação Olá após algum tempo. |Esse erro indica que a autenticação com ACS foi aprovada, mas Olá register chamada feita toohello serviço falhou. Isso pode ser resultado de uma falha de rede esporádica. |Se o problema de saudação persistir, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md). |
| 4 |Erro 350049: o serviço de saudação não pôde ser alcançado durante o registro. |Quando é feita a chamada de saudação de serviço toohello, uma exceção da web é recebida. Em alguns casos, isso pode obter corrigido repetindo a operação hello mais tarde. |Verifique seu endereço IP e o nome DNS e, em seguida, repita a operação de saudação. Se Olá problema persistir, [entre em contato com o Microsoft Support.](storsimple-contact-microsoft-support.md) |
| 5 |Erro 350031: dispositivo Olá já foi registrado. | |Nenhuma ação é necessária. |
| 6 |Erro 350016: falha no registro do dispositivo. | |Verifique se a chave de registro hello está correto. |
| 7 |Invoke-HcsSetupWizard: Ocorreu um erro ao registrar seu dispositivo. Isso pode ser devido a nome DNS ou endereço IP tooincorrect. Verifique suas configurações de rede e tente novamente. Se Olá problema persistir, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md). (Erro 350050) |Certifique-se de que o dispositivo pode executar ping Olá fora da rede. Se você tiver conectividade toooutside rede, registro Olá pode falhar com o erro. Esse erro pode ser uma combinação de um ou mais dos seguintes hello:<ul><li>IP incorreto</li><li>Sub-rede incorreta</li><li>Gateway incorreto</li><li>Configurações de DNS incorretas</li></ul> |Consulte etapas Olá Olá [exemplo passo a passo de solução de problemas](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard: Olá atual falha na operação devido a erro de serviço interno tooan [0x1FBE2]. Repita a operação Olá após algum tempo. Se Olá problema persistir, entre em contato com o Microsoft Support. |Esse é um erro genérico lançado para todos os erros de usuário invisíveis do serviço ou agente. motivo mais comum de saudação pode ser que a autenticação Olá ACS falhou. Uma possível causa da falha de saudação é que há problemas com a configuração do servidor NTP hello e horário no dispositivo de saudação não está definido corretamente. |Corrija o tempo de saudação (se houver problemas) e, em seguida, repita a operação de registro de saudação. Se você usar Olá Set-HcsSystem - fuso horário comando tooadjust Olá fuso horário, cada palavra em maiuscula no fuso horário de saudação (por exemplo "Hora padrão").  Se o problema persistir, [contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para as próximas etapas. |
| 9 |Aviso: Não foi possível ativar o dispositivo hello. As senhas do administrador do dispositivo e do Gerenciador de Instantâneos StorSimple não foram alteradas. |Se o registro de saudação falhar, administrador do dispositivo hello e senhas do Gerenciador de instantâneos do StorSimple não são alteradas. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Ferramentas para solucionar problemas em implantações do StorSimple
StorSimple inclui várias ferramentas que você pode usar tootroubleshoot sua solução StorSimple. Estão incluídos:

* Pacotes de suporte e logs de dispositivo 
* Cmdlets projetados especificamente para a solução de problemas 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Pacotes de suporte e logs de dispositivo disponíveis para solução de problemas
Um pacote de suporte contém todos os logs de saudação relevantes que podem ajudar a equipe do Microsoft Support Olá com solução de problemas do dispositivo. Você pode usar o Windows PowerShell para StorSimple toogenerate um pacote de suporte criptografado que pode ser compartilhado com a equipe de suporte.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>tooview Olá logs ou conteúdo Olá Olá do pacote de suporte
1. Usar o Windows PowerShell para StorSimple toogenerate um pacote de suporte, conforme descrito em [criar e gerenciar um pacote de suporte](storsimple-create-manage-support-package.md).
2. Baixar Olá [script descriptografia](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente no computador cliente.
3. Use este [procedimento passo a passo](storsimple-create-manage-support-package.md#edit-a-support-package) pacote de suporte Olá tooopen e descriptografar.
4. Olá descriptografada logs estão no formato de etw/etvx do pacote de suporte. Você pode executar Olá tooview as etapas a seguir esses arquivos no Visualizador de eventos do Windows:
   
   1. Executar Olá **eventvwr** comando no cliente do Windows. Isso iniciará a saudação Visualizador de eventos.
   2. Em Olá **ações** painel, clique em **Abrir Log salvo** e arquivos de log do ponto toohello no formato etvx/etw (pacote de suporte de saudação). Agora você pode exibir o arquivo hello. Depois de abrir o arquivo hello, você pode com o botão direito e salve o arquivo hello como texto.
      
      > [!IMPORTANT]
      > Você também pode usar o hello **Get-WinEvent** tooopen cmdlet esses arquivos no Windows PowerShell. Para obter mais informações, consulte [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) em Olá documentação de referência de cmdlet do Windows PowerShell.
      > 
      > 
5. Ao abrir Olá logs no Visualizador de eventos, procure Olá logs que contêm a configuração do dispositivo toohello relacionados problemas a seguir:
   
   * hcs_pfconfig/Operational Log
   * hcs_pfconfig/Config
6. Nos arquivos de log hello, pesquise cadeias de caracteres cmdlets relacionados toohello chamado pelo Assistente de instalação de saudação. Consulte [Processo do assistente de instalação inicial](#first-time-setup-wizard-process) para obter uma lista desses cmdlets. 
7. Se você não for capaz de toofigure out causa de saudação do problema hello, você pode [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) para as próximas etapas. Olá Use as etapas em [criar uma solicitação de suporte](storsimple-contact-microsoft-support.md#create-a-support-request) quando você contatar o Microsoft Support para obter assistência.

## <a name="cmdlets-available-for-troubleshooting"></a>Cmdlets disponíveis para solução de problemas
Saudação de usar os seguintes erros de conectividade de toodetect de cmdlets do Windows PowerShell.

* `Get-NetAdapter`: Use esse cmdlet da integridade Olá toodetect de interfaces de rede. 
* `Test-Connection`: Use essa conectividade de rede do cmdlet toocheck hello dentro e fora da rede hello.
* `Test-HcsmConnection`: Use essa conectividade de saudação do cmdlet toocheck de um dispositivo registrado com êxito.

Se você estiver executando a atualização 1 em seu dispositivo StorSimple, Olá cmdlets de diagnóstico a seguir também está disponível.

* `Sync-HcsTime`: Use essa hora do dispositivo toodisplay cmdlet e forçar uma sincronização com o servidor NTP hello.
* `Enable-HcsPing`e `Disable-HcsPing`: usar essas interfaces de rede cmdlets tooallow Olá hosts tooping Olá em seu dispositivo StorSimple. Por padrão, interfaces de rede Olá StorSimple não responder solicitações tooping.
* `Trace-HcsRoute`: Use este cmdlet como uma ferramenta de rastreamento de rota. Ele envia o roteador de tooeach de pacotes no destino final da saudação maneira tooa durante um período de tempo e depois calcula os resultados com base em pacotes de saudação retornados de cada salto. Como `Trace-HcsRoute` mostra o grau de saudação de perda de pacotes em qualquer determinado roteador ou link, você pode identificar quais roteadores ou links que possam estar causando problemas de rede. 
* `Get-HcsRoutingTable`: Use esse cmdlet toodisplay Olá tabela roteamento IP local.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Solucionar problemas com o cmdlet Get-NetAdapter de saudação
Quando você configura interfaces de rede para uma implantação de dispositivo pela primeira vez, status do hardware Olá não está disponível no hello serviço StorSimple Manager da interface do usuário porque o dispositivo Olá ainda não foi registrado com o serviço de saudação. Além disso, página de Status do Hardware Olá pode não refletir corretamente estado de saudação do dispositivo hello, especialmente se houver problemas que afetam a sincronização do serviço. Nessas situações, você pode usar o hello `Get-NetAdapter` toodetermine cmdlet Olá integridade e o status das suas interfaces de rede.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee uma lista de todos os adaptadores de rede Olá no seu dispositivo
1. Inicie o Windows PowerShell para StorSimple e digite `Get-NetAdapter`. 
2. Usar a saída de saudação do hello `Get-NetAdapter` cmdlet e hello toounderstand diretrizes a seguir Olá status de sua interface de rede.
   
   * Se a interface hello está íntegra e habilitada, Olá **ifIndex** status será mostrado como **backup**.
   * Se a interface hello está íntegra, mas não está conectada fisicamente (por um cabo de rede), Olá **ifIndex** é mostrado como **desabilitado**.
   * Se a interface hello está íntegra, mas não habilitado, Olá **ifIndex** status será mostrado como **NotPresent**.
   * Se a interface de saudação não existir, ele não aparecer nessa lista. Olá serviço StorSimple Manager da interface do usuário ainda mostrará essa interface em um estado de falha.

Para obter mais informações sobre como toouse esse cmdlet, vá muito[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) em Olá referência de cmdlet do Windows PowerShell. 

Olá, seções a seguir mostram exemplos de saída de hello `Get-NetAdapter` cmdlet. 

 Nesses exemplos, controlador 0 foi o controlador passivo hello e foi configurado da seguinte maneira:

* DATA 0, DATA 1, DATA 2 e DATA 3 rede interfaces existiam no dispositivo de saudação.
* DATA 4 e 5 dados placas de interface de rede não estavam presentes; Portanto, eles não são listados na saída de hello.
* DADOS 0 estava habilitada.

Controlador 1 foi o controlador ativo hello e foi configurado da seguinte maneira:

* DATA 0, DATA 1, dados 2, 3 de dados, DATA 4 e DATA 5 rede interfaces existiam no dispositivo de saudação.
* DADOS 0 estava habilitada.

**Saída de exemplo – controlador 0**

seguir Olá é saída de saudação do controlador 0 (controlador de passivo Olá). DADOS 1, DADOS 2 e DADOS 3 não estão conectadas. DATA 4 e 5 dados não são listadas porque eles não estão presentes no dispositivo de saudação. 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Saída de exemplo – controlador 1**

seguir Olá é saída de saudação do controlador 1 (controlador ativo do hello). Somente Olá DATA 0 interface de rede no dispositivo hello está configurado e funcionando.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Solucionar problemas com o cmdlet de Conexão de teste Olá
Você pode usar o hello `Test-Connection` toodetermine cmdlet se seu dispositivo StorSimple pode se conectar a toohello fora da rede. Se todos os parâmetros de rede hello, incluindo Olá DNS, estão configurados corretamente no Assistente de instalação hello, você pode usar o hello `Test-Connection` cmdlet tooping um endereço conhecido fora da rede hello, como outlook.com. 

Se o ping estiver desabilitado, você deve habilitar problemas de conectividade do ping tootroubleshoot com esse cmdlet.

Consulte Olá a seguir exemplos de saída de hello `Test-Connection` cmdlet. 

> [!NOTE]
> No primeiro exemplo de hello, dispositivo Olá é configurado com um DNS incorreto. No segundo exemplo de hello, Olá DNS está correta.
> 
> 

**Saída de exemplo – DNS incorreto**

Saudação de exemplo a seguir, não há nenhuma saída para endereços IPV4 e IPV6 hello, que indica que Olá que DNS não for resolvido. Isso significa que não há nenhum toohello conectividade fora da rede e um DNS correto precisa toobe fornecido. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Saída de exemplo – DNS correto**

Em Olá exemplo a seguir, Olá DNS retorna Olá endereço IPV4, indicando que Olá que DNS está configurado corretamente. Isso confirma que há conectividade toohello fora da rede. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Solucionar problemas com o cmdlet Test-HcsmConnection de saudação
Saudação de uso `Test-HcsmConnection` cmdlet para um dispositivo que já está conectado tooand registrado no serviço StorSimple Manager. Esse cmdlet ajuda a verificar a conectividade de saudação entre um dispositivo registrado e Olá correspondente serviço StorSimple Manager. Você pode executar esse comando no Windows PowerShell para StorSimple. 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>toorun Olá Test-HcsmConnection cmdlet
1. Certifique-se de que o dispositivo hello está registrado.
2. Verificar o status do dispositivo de saudação. Se o dispositivo hello está desativado, no modo de manutenção ou offline, você poderá ver Olá os erros a seguir: 
   
   * Cisdevicedecommissioned – indica que o dispositivo hello está desativado.
   * Devicenotready – indica que o dispositivo hello está no modo de manutenção.
   * Devicenotready – indica que o dispositivo Olá não está online.
3. Verifique se esse Olá serviço StorSimple Manager está em execução (use Olá [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet). Se o serviço de saudação não está em execução, você poderá ver Olá os erros a seguir:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError – indica que houve uma exceção ao executar Get-ClusterResource.
4. Verifique o token de serviço de controle de acesso (ACS) hello. Se ele lança uma exceção de web, ele pode ser resultado de saudação de um problema de gateway, a autenticação de proxy ausentes, um DNS incorreto ou uma falha de autenticação. Você poderá ver Olá os erros a seguir:
   
   * ErrorCode. Cisappliancegateway – isso indica uma exceção httpstatuscode. Badgateway: serviço de resolução de nome de saudação não foi possível resolver o nome do host hello. 
   * ErrorCode. Cisapplianceproxy – isso indica uma exceção httpstatuscode. Proxyauthenticationrequired (código de status HTTP 407): cliente Olá não foi possível autenticar com o servidor de proxy de saudação. 
   * ErrorCode. Cisappliancednserror – isso indica uma exceção WebExceptionStatus. Nameresolutionfailure: serviço de resolução de nome de saudação não foi possível resolver o nome do host hello.
   * Cisapplianceacserror – indica que Olá serviço retornou um erro de autenticação, mas não há conectividade.
     
     Se isso não lançar uma exceção da Web, procure um ErrorCode.CiSApplianceFailure. Isso indica que esse dispositivo Olá falhou.
5. Verifique a conectividade do serviço de nuvem hello. Se o serviço hello gera uma exceção de web, você poderá ver Olá os erros a seguir:
   
   * ErrorCode. Cisappliancegateway – isso indica uma exceção httpstatuscode. Badgateway: um servidor proxy intermediário recebeu uma solicitação incorreta de outro proxy ou do servidor de saudação original.
   * ErrorCode. Cisapplianceproxy – isso indica uma exceção httpstatuscode. Proxyauthenticationrequired (código de status HTTP 407): cliente Olá não foi possível autenticar com o servidor de proxy de saudação. 
   * ErrorCode. Cisappliancednserror – isso indica uma exceção WebExceptionStatus. Nameresolutionfailure: serviço de resolução de nome de saudação não foi possível resolver o nome do host hello.
   * Cisapplianceacserror – indica que Olá serviço retornou um erro de autenticação, mas não há conectividade.
     
     Se isso não lançar uma exceção da Web, procure um ErrorCode.CiSApplianceSaasServiceErro. Isso indica um problema com hello serviço StorSimple Manager.
6. Verifique a conectividade do Barramento de Serviço do Azure. Cisapplianceservicebuserror indica que o dispositivo Olá não pode se conectar a toohello barramento de serviço.

Olá arquivos de log Ciscommandletlog0curr e Cisagentsvc0curr terão mais informações, como detalhes da exceção. 

Para obter mais informações sobre como toouse Olá cmdlet, vá muito[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) documentação de referência de saudação do Windows PowerShell.

> [!IMPORTANT]
> Você pode executar este cmdlet para Olá ativo e o controlador passivo hello. 
> 
> 

Consulte Olá a seguir exemplos de saída de hello `Test-HcsmConnection` cmdlet. 

**Exemplo de saída – dispositivo registrado com êxito, executando a versão do StorSimple (julho de 2014)**

Olá primeiro exemplo é de um dispositivo que está registrado com êxito com hello serviço StorSimple Manager e não tem nenhum problema de conectividade. 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**Exemplo de saída – Dispositivo que executa o StorSimple Atualização 1 registrado com êxito**

Se você estiver executando a atualização 1 em seu dispositivo StorSimple, você não precisará toorun-lo com a opção detalhada hello.

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Exemplo de saída – dispositivo offline, executando a versão do StorSimple (julho de 2014)**

Este exemplo é de um dispositivo que tem um status de **Offline** em Olá portal clássico do Azure.

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

Olá dispositivo não pôde se conectar usando a configuração atual de proxy da web hello. Isso pode ser um problema com a configuração do proxy web hello ou um problema de conectividade de rede. Nesse caso, certifique-se de que as configurações de proxy da web estejam corretas e de que seus servidores de proxy da Web estão online e acessíveis. 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Solucionar problemas com o cmdlet de sincronização HcsTime Olá
Use o cmdlet toodisplay Olá dispositivo momento. Se a hora do dispositivo Olá tem um deslocamento com o servidor NTP hello, você pode usar este cmdlet tooforce-sincronizar o tempo de saudação com o servidor NTP. Se o deslocamento de saudação entre o servidor NTP e dispositivo Olá for maior que 5 minutos, você verá um aviso. Se o deslocamento de saudação exceder 15 minutos, dispositivo Olá ficará offline. Você ainda pode usar esse cmdlet tooforce uma sincronização de horário. No entanto, se o deslocamento Olá exceder 15 horas, em seguida, você não será capaz de sincronização de tooforce tempo de saudação e uma mensagem de erro será mostrada.

**Exemplo de saída – sincronização de tempo forçada usando o Sync-HcsTime**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Solucionar problemas com os cmdlets do HcsPing habilitar e desabilitar HcsPing Olá
Use esses tooensure cmdlets interfaces de rede de saudação em seu dispositivo respondem tooICMP solicitações de ping. Por padrão interfaces de rede Olá StorSimple não responder solicitações tooping. Usar esse cmdlet é Olá tooknow de maneira mais fácil se seu dispositivo está online e acessível.  

**Exemplo de saída – Enable-HcsPing e Disable-HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Solucionar problemas com o cmdlet de rastreamento HcsRoute Olá
Use este cmdlet como uma ferramenta de rastreamento de rota. Ele envia o roteador de tooeach de pacotes no destino final da saudação maneira tooa durante um período de tempo e depois calcula os resultados com base em pacotes de saudação retornados de cada salto. Como Olá cmdlet indica o grau de saudação de perda de pacotes em um determinado roteador ou link, você pode identificar quais roteadores ou links que possam estar causando problemas de rede.

**Saída de exemplo mostrando como tootrace Olá rota de um pacote com HcsRoute de rastreamento**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Solucionar problemas com o cmdlet de Get-HcsRoutingTable Olá
Use essa tabela de roteamento de saudação do cmdlet tooview para seu dispositivo StorSimple. Uma tabela de roteamento é um conjunto de regras que pode ajudar a determinar para onde os pacotes de dados transmitidos em uma rede IP (protocolo IP) serão direcionados. 

tabela de roteamento Hello mostra interfaces hello e gateway rotas Olá dados toohello hello especificado redes. Ele também fornece a métrica de roteamento de saudação que é o tomador de decisões Olá para Olá caminho tomado tooreach um destino específico. Olá inferior Olá roteamento métrica, Olá Olá preferência maior. 

Por exemplo, se você tiver 2 interfaces de rede DATA 2 e DATA 3, toohello conectado à Internet. Se a métrica de roteamento Olá para DATA 2 e DATA 3 é 15 e 261, respectivamente, DATA 2 com a métrica de roteamento menor Olá é interface preferencial do hello usado Olá tooreach da Internet.

Se você estiver executando a atualização 1 em seu dispositivo StorSimple, sua interface de rede 0 de dados tem a preferência mais alta Olá para o tráfego de nuvem hello. Isso significa que mesmo se houver outras interfaces de nuvem habilitada, o tráfego de nuvem Olá será encaminhado por meio de dados 0. 

Se você executar Olá `Get-HcsRoutingTable` cmdlet sem especificar quaisquer parâmetros (como Olá mostrado no exemplo a seguir), Olá cmdlet mostrará tabelas de roteamento de IPv4 e IPv6. Como alternativa, você pode especificar `Get-HcsRoutingTable -IPv4` ou `Get-HcsRoutingTable -IPv6` tooget uma tabela de roteamento relevante.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Exemplo passo a passo de solução de problemas do StorSimple
Olá exemplo a seguir mostra passo a passo de solução de problemas de uma implantação do StorSimple. No cenário de exemplo hello, registro de dispositivo falhará com uma mensagem de erro indicando que as configurações de rede hello ou nome DNS hello está incorreto.

mensagem de saudação do erro retornada é:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Erro de saudação pode ser causado por qualquer uma das seguintes hello:

* Instalação de hardware incorreto
* Interfaces de rede com defeito
* Endereço IP, máscara de sub-rede, gateway, servidor DNS primário ou proxy da Web incorreto
* Chave de registro incorreta
* Configurações de firewall incorretas

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>problema de registro de dispositivo Olá toolocate e correção
1. Verifique a configuração do dispositivo: no controlador ativo do hello, execute `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > Assistente de instalação Olá deve executar no controlador ativo hello. tooverify que são o controlador ativo conectado toohello, examinar a faixa de saudação apresentada no console serial hello. Faixa de saudação indica se você está conectado toocontroller 0 ou controlador 1 e se o controlador hello está ativo ou passivo. Para obter mais informações, vá muito[identificar um controlador ativo em seu dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
   > 
   > 
2. Certifique-se de que o dispositivo hello está conectado corretamente: verificar Olá cabeamento de rede no dispositivo de saudação plano posterior. Olá cabeamento é específico toohello modelo do dispositivo. Para obter mais informações, vá muito[instalar seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) ou [instalar seu dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > Se você estiver usando portas de rede 10 GbE, você precisará Olá toouse fornecido cabos SFP e adaptadores de QSFP-SFP. Para obter mais informações, consulte Olá [lista de cabos, comutadores e transceptores recomendados para as portas do hello 10 GbE](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
   > 
   > 
3. Verificar integridade Olá Olá da interface de rede:
   
   * Use a integridade de saudação de toodetect Olá Get-NetAdapter cmdlet Olá de interfaces de rede para DATA 0. 
   * Se o link de saudação não estiver funcionando, Olá **ifindex** status indicará essa interface hello está inativa. Conexão de rede toocheck Olá de dispositivo de toohello Olá porta e comutador toohello, em seguida, será necessário. Você também precisará toorule out cabos incorretos. 
   * Se você suspeitar que Olá DATA 0 no controlador ativo Olá falhou, você pode confirmar isso conectando-se toohello a porta DATA 0 no controlador 1. tooconfirm isso, desconecte o cabo de rede Olá Olá parte posterior do dispositivo de saudação do controlador 0, conectar Olá cabo toocontroller 1 e, em seguida, execute o cmdlet de Olá Get-NetAdapter novamente. 
     Se Olá DATA 0 porta em um controlador falha, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) para as próximas etapas. Talvez seja necessário controlador de saudação tooreplace em seu sistema.
4. Verifique se o comutador de toohello conectividade hello:
   
   * Certifique-se de que dados interfaces de rede 0 no controlador 0 e 1 no seu compartimento primário estão em Olá mesma sub-rede. 
   * Verifique Olá hub ou roteador. Normalmente, você deve se conectar a ambos os controladores toohello mesmo hub ou roteador. 
   * Certifique-se de que opções de saudação usadas para conexão Olá têm DATA 0 para ambos os controladores em Olá mesma vLAN.
5. Elimine erros de usuário:
   
   * Execute novamente o Assistente de instalação da saudação (executar **Invoke-HcsSetupWizard**) e digite Olá novamente valores toomake-se de que não existem erros. 
   * Verificar o registro de saudação chave usada. Olá a mesma chave de registro pode ser usado tooconnect vários dispositivos tooa serviço StorSimple Manager. Use o procedimento Olá [chave de registro de serviço Get hello](storsimple-manage-service.md#get-the-service-registration-key) Olá tooensure que você está usando a chave de registro correta.
     
     > [!IMPORTANT]
     > Se você tiver vários serviços em execução, será necessário tooensure essa chave de registro Olá para serviço apropriado Olá é o dispositivo de saudação tooregister usado. Se você registrou um dispositivo com o serviço StorSimple Manager incorreto de saudação, será necessário muito[entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) para as próximas etapas. Você pode ter uma redefinição de fábrica do dispositivo da saudação (que pode resultar em perda de dados) tooperform toothen conecte-o serviço toohello se destina.
     > 
     > 
6. Use tooverify de cmdlet Olá Conexão de teste que você tem conectividade toohello fora da rede. Para obter mais informações, vá muito[solução de problemas com o cmdlet Olá Conexão de teste](#troubleshoot-with-the-test-connection-cmdlet).
7. Verifique se há interferência de firewall. Se você tiver verificado que Olá virtual configurações de IP (VIP), sub-rede, gateway e DNS estão corretas e ainda vê problemas de conectividade, é possível que seu firewall está bloqueando a comunicação entre o dispositivo e Olá fora da rede. Você precisa de tooensure que as portas 80 e 443 estão disponíveis em seu dispositivo StorSimple para comunicação de saída. Para obter mais informações, consulte os [Requisitos de rede do dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Examine os logs de saudação. Vá muito[dão suporte a pacotes e logs de dispositivo disponíveis para solução de problemas](#support-packages-and-device-logs-available-for-troubleshooting).
9. Se hello etapas anteriores não resolverem o problema Olá, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) para obter assistência.

## <a name="next-steps"></a>Próximas etapas
[Saiba como tootroubleshoot um dispositivo operacional](storsimple-troubleshoot-operational-device.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
