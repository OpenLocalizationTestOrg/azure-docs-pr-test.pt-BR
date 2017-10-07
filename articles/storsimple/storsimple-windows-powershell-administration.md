---
title: aaaPowerShell para gerenciamento de dispositivo do StorSimple | Microsoft Docs
description: Saiba como toouse do Windows PowerShell para StorSimple toomanage seu dispositivo StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0ff3bb0d-897a-4676-bdcb-402c2628dac5
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 1adcbb8bb89e3e3b4f328aac198690476c2a78cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Usar o Windows PowerShell para StorSimple tooadminister seu dispositivo
## <a name="overview"></a>Visão geral
O Windows PowerShell para StorSimple fornece uma interface de linha de comando que você pode usar toomanage seu dispositivo StorSimple do Microsoft Azure. Como Olá nome sugere, é uma interface de linha de comando baseado no Windows PowerShell, que é criada em um runspace restrito. Da perspectiva de saudação do usuário Olá na linha de comando hello, um runspace com restrição aparece como uma versão restrita do Windows PowerShell. Ao mesmo tempo que mantém alguns dos recursos básicos de saudação do Windows PowerShell, essa interface possui cmdlets dedicados que se destinam a gerenciar seu dispositivo StorSimple do Microsoft Azure. 

Este artigo descreve saudação do Windows PowerShell para StorSimple recursos, incluindo como você pode se conectar a interface toothis e contém procedimentos de toostep-a-passo links ou fluxos de trabalho que você pode executar usando esta interface. fluxos de trabalho de saudação incluem como a tooregister seu dispositivo, configurar a interface de rede de saudação em seu dispositivo, instale as atualizações que exigem Olá toobe de dispositivo no modo de manutenção, alterar o estado do dispositivo Olá, e solucionar problemas que podem ocorrer.

Neste artigo, você aprenderá a:

* Conecte o dispositivo StorSimple tooyour usando o Windows PowerShell para StorSimple.
* Administre o seu dispositivo StorSimple usando o Windows PowerShell para StorSimple.
* Obtenha ajuda no Windows PowerShell para StorSimple.

> [!NOTE]
> * O Windows PowerShell para StorSimple cmdlets permitem que você toomanage seu dispositivo StorSimple do console de série ou remotamente por meio de comunicação remota do Windows PowerShell. Para obter mais informações sobre cada Olá cmdlets individuais que podem ser usados nesta interface, vá muito[referência de cmdlet do Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * Olá StorSimple do Azure PowerShell cmdlets são um conjunto diferente de cmdlets que permitem que você tooautomate nível de serviço do StorSimple e tarefas de migração da linha de comando de saudação. Para obter mais informações sobre Olá cmdlets do Azure PowerShell para StorSimple, vá toohello [referência de cmdlet do Azure StorSimple](/powershell/module/azure/?view=azuresmps-3.7.0).
> 
> 

Você pode acessar a saudação do Windows PowerShell para StorSimple usando um dos métodos a seguir de saudação:

* [Conecte-se o console serial do dispositivo tooStorSimple](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Conectar-se remotamente tooStorSimple usando o Windows PowerShell](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Conecte-se tooWindows do PowerShell para StorSimple por meio do console serial do dispositivo Olá
Você pode [baixar PuTTY](http://www.putty.org/) ou similar tooWindows de tooconnect de software de emulação de terminal do PowerShell para StorSimple. Você precisa tooconfigure PuTTY especificamente tooaccess Olá dispositivo StorSimple do Microsoft Azure. Olá, tópicos a seguir contêm etapas detalhadas sobre como tooconfigure PuTTy e conecte-se o dispositivo toohello. Várias opções de menu no console serial Olá também são explicadas.

### <a name="putty-settings"></a>Configurações do PuTTY
Certifique-se de que você use Olá após a interface do Windows PowerShell do configurações de PuTTY tooconnect toohello do console serial hello.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY
1. Em Olá PuTTY **reconfiguração** caixa de diálogo Olá **categoria** painel, selecione **teclado**.
2. Certifique-se de que Olá as opções a seguir estão selecionadas (essas são as configurações padrão de saudação quando você inicia uma nova sessão). 
   
   | Item de teclado | Selecionar |
   | --- | --- |
   | Tecla BACKSPACE |Control-? (127) |
   | Teclas Home e End |Standard |
   | Teclado numérico e teclas de função |ESC[n~ |
   | Estado inicial das teclas de cursor |Normal |
   | Estado inicial do teclado numérico |Normal |
   | Habilitar recursos adicionais do teclado |Control-Alt é diferente de AltGr |
   
    ![Configurações do Putty permitidas](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Clique em **Aplicar**.
4. Em Olá **categoria** painel, selecione **tradução**.
5. Em Olá **conjunto de caracteres remotos** caixa de listagem, selecione **UTF-8**.
6. Em **Manipulação de caracteres de desenho** de linha, selecione **Use pontos de código de desenho de linha Unicode**. Olá ilustração a seguir mostra seleções corretas do PuTTY hello.
   
    ![Configurações do PuTTY UTF](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Clique em **Aplicar**.

Agora você pode usar o console serial do dispositivo tooconnect PuTTY toohello fazendo Olá etapas a seguir.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Sobre o console serial Olá
Quando você acessar a interface do Windows PowerShell de saudação do seu dispositivo StorSimple por meio do console serial hello, uma mensagem de faixa é apresentada, seguida por opções de menu. 

mensagem faixa contém informações básicas de dispositivo StorSimple como modelo Olá, nome, versão do software instalado e status do controlador de saudação que você está acessando. Olá a imagem a seguir mostra um exemplo de uma mensagem de faixa.

![Mensagem da faixa serial](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> Você pode usar o hello tooidentify de mensagem de faixa se Olá controlador que você está conectado toois ativo ou passivo.
> 
> 

Olá imagem mostra a seguir Olá várias opções de runspace disponíveis no menu do console serial hello.

![Registrar seu dispositivo 2](./media/storsimple-windows-powershell-administration/IC740906.png)

Você pode escolher Olá configurações a seguir:

1. **Faça logon com acesso completo** essa opção permite que você tooconnect (com as credenciais apropriadas Olá) toohello **SSAdminConsole** runspace no controlador de local de saudação. (Olá local é Olá controlador que você está acessando por meio do console serial do seu dispositivo StorSimple hello.) Essa opção também pode ser usada tooallow Microsoft Support tooaccess irrestrito runspace (uma sessão de suporte) tootroubleshoot possíveis problemas do dispositivo. Depois de usar a opção 1 toolog em, você pode permitir que Olá Microsoft Support engenheiro runspace tooaccess irrestrito ao executar um cmdlet específico. Para obter detalhes, consulte muito[iniciar uma sessão de suporte](storsimple-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
2. **Faça logon no controlador de toopeer com acesso completo** essa opção é Olá igual à opção 1, exceto que você pode se conectar (com as credenciais apropriadas Olá) toohello **SSAdminConsole** runspace no controlador de par de saudação. Como o dispositivo StorSimple Olá é um dispositivo de alta disponibilidade com dois controladores em uma configuração ativa-passiva, par refere-se toohello outro controlador no dispositivo Olá que você está acessando por meio do console serial Olá).
   Semelhante toooption 1, essa opção também pode ser usado tooallow Microsoft Support tooaccess irrestrito runspace em um controlador de par.
3. **Conecte-se com acesso limitado** essa opção é usada tooaccess interface do Windows PowerShell no modo limited. As credenciais de acesso não são solicitadas. Esta opção conecta tooa mais restringido runspace comparado toooptions 1 e 2.  Algumas das tarefas de saudação que estão disponíveis por meio da opção 1 que **não é possível* ser realizadas no runspace são:
   
   * Redefinir as configurações de fábrica toohello
   * Alterar a senha Olá
   * Habilitar ou desabilitar o acesso de suporte
   * Aplicar atualizações
   * Instale hotfixes 

    > [!NOTE]
    > Isso é a opção Olá preferido se você tiver esquecido a senha de administrador do dispositivo hello e não pode se conectar por meio da opção 1 ou 2.

4. **Alterar idioma** essa opção permite que você toochange idioma de exibição Olá na interface do Windows PowerShell hello. idiomas Olá com suporte são inglês, japonês, russo, francês, Sul-coreano, espanhol, italiano, alemão, chinês e português (Brasil).

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Conectar-se remotamente tooStorSimple usando o Windows PowerShell para StorSimple
Você pode usar o dispositivo StorSimple do Windows PowerShell remoting tooconnect tooyour. Ao se conectar dessa maneira, você não verá um menu. (Você verá um menu somente se você usar o console serial Olá em Olá dispositivo tooconnect. Conectar-se remotamente leva diretamente toohello equivalente de "opção 1 – acesso completo" no console serial hello.) Com a comunicação remota do Windows PowerShell, você pode se conectar runspace específico tooa. Você também pode especificar o idioma de exibição de saudação. 

Olá idioma de exibição é independente do idioma de saudação que você define usando Olá **alterar idioma** opção no menu do console serial hello. PowerShell remoto escolherá automaticamente a localidade de saudação do dispositivo hello que está se conectando de se nenhum for especificado.

> [!NOTE]
> Se você estiver trabalhando com hosts virtuais do Microsoft Azure e dispositivos virtuais StorSimple, você pode usar o Windows PowerShell remoting e hello host virtual tooconnect toohello dispositivo virtual. Se você tiver configurado um local de compartilhamento no host de saudação toosave informações de sessão do Windows PowerShell hello, você deve estar ciente de que Olá que todos principal inclui somente os usuários autenticados. Portanto, se você configurou o acesso ao compartilhamento de tooallow Olá por todos os usuários e conecte-se sem especificar credenciais, principal anônimas não autenticadas de saudação será usado e você verá um erro. toofix esse problema, em Olá compartilhar host, você deve habilitar a conta de convidado hello e dar a cota de toohello Olá convidado conta acesso completo ou você deve especificar credenciais válidas juntamente com hello cmdlet do Windows PowerShell.
> 
> 

Você pode usar HTTP ou HTTPS tooconnect via comunicação remota do Windows PowerShell. Use instruções Olá Olá tutoriais a seguir:

* [Conectar-se remotamente usando HTTP](storsimple-remote-connect.md#connect-through-http)
* [Conectar-se remotamente usando HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Considerações de segurança de conexão
Ao decidir como tooconnect tooWindows PowerShell para StorSimple, considere o seguinte hello:

* Conectando-se diretamente toohello console serial do dispositivo é seguro, mas conectar console serial do toohello em comutadores de rede não é. Seja cauteloso Olá dos riscos de segurança ao conectar-se a série de toodevice em comutadores de rede.
* Conectando por meio de uma sessão HTTP pode oferecer mais segurança do que conectar-se por meio do console serial Olá via rede. Embora isso não é um método mais seguro Olá, é aceitável em redes confiáveis.
* Conectando por meio de uma sessão HTTPS é hello mais seguro e Olá opção recomendada.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Administrar o seu dispositivo StorSimple usando o Windows PowerShell para StorSimple
Olá tabela a seguir mostra um resumo de todas as tarefas comuns de gerenciamento hello e fluxos de trabalho complexos que podem ser executados na interface do Windows PowerShell de saudação do seu dispositivo StorSimple. Para obter mais informações sobre cada fluxo de trabalho, clique Olá devida entrada na tabela de saudação.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Fluxos de trabalho do Windows PowerShell para StorSimple
| Se você deseja toodo... | Utilize este procedimento. |
| --- | --- |
| Registre seu dispositivo |[Configurar e registrar dispositivo hello usando o Windows PowerShell para StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Configurar o proxy Web</br>Exibir configurações do proxy Web |[Configurar proxy da web para seu dispositivo StorSimple](storsimple-configure-web-proxy.md) |
| Modificar as configurações de interface de rede DATA 0 em seu dispositivo StorSimple |[Modificar a interface de rede DATA 0 em seu dispositivo StorSimple](storsimple-modify-data-0.md) |
| Parar um controlador  </br> Reiniciar ou desligar um controlador </br> Desligar um dispositivo</br>Redefinir as configurações padrão do hello dispositivo toofactory |[Gerenciar os controladores do dispositivo](storsimple-manage-device-controller.md) |
| Instalar atualizações e hotfixes no modo de manutenção |[Atualizar seu dispositivo](storsimple-update-device.md) |
| Entrar no modo de manutenção  </br>Sair do modo de manutenção |[Modos de dispositivo StorSimple](storsimple-device-modes.md) |
| Criar um pacote de Suporte</br>Descriptografar e editar um pacote de suporte |[Criar e gerenciar pacotes de suporte](storsimple-create-manage-support-package.md) |
| Iniciar uma sessão de suporte</br> |[Iniciar uma sessão de suporte no Windows PowerShell para StorSimple](storsimple-create-manage-support-package.md#manually-create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Obter ajuda no Windows PowerShell para StorSimple
No Windows PowerShell para StorSimple, a Ajuda de cmdlet está disponível. Uma versão online atualizada desta ajuda também está disponível, que você pode usar tooupdate Olá Ajuda em seu sistema.

Obtendo ajuda nesta interface é semelhante toothat no Windows PowerShell e a maioria das Olá cmdlets relacionados à Ajuda funcionará. Você pode encontrar ajuda para o Windows PowerShell online na Biblioteca TechNet do hello: [scripts com o Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).

a seguir Olá é uma breve descrição dos tipos de saudação de ajuda para a interface do Windows PowerShell, incluindo como tooupdate Olá ajuda.

#### <a name="tooget-help-for-a-cmdlet"></a>tooget ajuda para um cmdlet
* tooget ajuda para qualquer cmdlet ou função, use Olá comando a seguir:`Get-Help <cmdlet-name>`
* tooget ajuda online para qualquer cmdlet, usar o cmdlet anterior Olá com hello `-Online` parâmetro:`Get-Help <cmdlet-name> -Online`
* Para obter ajuda completa, você pode usar o hello `–Full` parâmetro e para obter exemplos, use Olá `–Examples` parâmetro.

#### <a name="tooupdate-help"></a>tooupdate ajuda
Você pode atualizar facilmente Olá ajuda na interface do Windows PowerShell hello. Execute Olá seguindo as etapas tooupdate Olá Ajuda em seu sistema.

#### <a name="tooupdate-cmdlet-help"></a>Ajuda do cmdlet tooupdate
1. Inicie o Windows PowerShell com hello **executar como administrador** opção.
2. No prompt de comando hello, digite:`Update-Help`
3. Olá atualizado ajuda os arquivos serão instalados.
4. Depois que os arquivos de ajuda de saudação são instalados, digite: `Get-Help Get-Command`. Isso exibirá uma lista dos cmdlets para os quais a Ajuda está disponível.

> [!NOTE]
> tooget uma lista de todos os cmdlets de saudação disponíveis em um runspace, faça logon na opção de menu correspondente toohello e execute Olá `Get-Command` cmdlet.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Se você tiver problemas com seu dispositivo StorSimple ao realizar uma saudação acima fluxos de trabalho, consulte muito[ferramentas para solucionar problemas de implantações de StorSimple](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

