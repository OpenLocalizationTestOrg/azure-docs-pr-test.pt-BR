---
title: "configuração do dispositivo aaaModify Olá StorSimple 8000 series | Microsoft Docs"
description: "Descreve como toouse Olá tooreconfigure de serviço do Gerenciador de dispositivos de StorSimple um dispositivo StorSimple que já tenha sido implantado."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>Usar toomodify de serviço do Gerenciador de dispositivos de StorSimple Olá a configuração do dispositivo StorSimple

## <a name="overview"></a>Visão geral

Olá portal do Azure **configurações do dispositivo** seção Olá **configurações** folha contém todos os parâmetros de dispositivo de saudação que você pode reconfigurar em um dispositivo StorSimple que é gerenciado por um Gerenciador de dispositivo do StorSimple serviço. Este tutorial explica como você pode usar o hello **configurações** Olá tooperform de folha tarefas de nível de dispositivo a seguir:

* Modificar o nome amigável do dispositivo
* Modificar as configurações de hora do dispositivo
* Atribuir um DNS secundário
* Modificar as interfaces de rede
* Alternar ou reatribuir IPs

## <a name="modify-device-friendly-name"></a>Modificar o nome amigável do dispositivo

Você pode usar o nome de dispositivo de Olá Olá toochange portal do Azure e atribua a ele um nome amigável exclusivo de sua escolha. Saudação de uso **configurações gerais** folha em seu nome amigável do dispositivo no dispositivo toomodify hello. nome amigável da saudação pode conter quaisquer caracteres e pode ter no máximo 64 caracteres.

> [!NOTE] 
> Você só pode modificar o nome de dispositivo de saudação no hello portal do Azure antes da instalação de dispositivo de saudação completa. Após a conclusão da instalação mínima do dispositivo do hello, você não pode alterar o nome do dispositivo hello.

![Nome do dispositivo nas Configurações gerais](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

Um dispositivo StorSimple que é conectado toohello serviço do Gerenciador de dispositivos do StorSimple é atribuído um nome padrão. Olá geralmente reflete Olá o número de série do dispositivo hello. Por exemplo, um nome de dispositivo padrão que é de 15 caracteres, como 8600-SHX0991003G44HT indica a seguir hello:

* **8600** – indica o modelo de dispositivo hello.
* **SHX** – site de produção de hello indica.
* **0991003** - Indica um produto específico.
* **G44HT**- Olá últimos 5 dígitos são incrementados toocreate números de série exclusivos. Isso pode não ser um conjunto sequencial.

## <a name="modify-device-description"></a>Modificar a descrição do dispositivo

Saudação de uso **configurações gerais** folha na descrição do dispositivo seu dispositivo toomodify hello.

![Descrição do dispositivo em configurações gerais](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

Uma descrição do dispositivo geralmente ajuda a identificar o proprietário hello e a localização física de saudação do dispositivo hello. campo de descrição de saudação deve conter menos de 256 caracteres.

## <a name="modify-time-settings"></a>Modificar as configurações de tempo

O dispositivo deve sincronizar o tempo em ordem tooauthenticate com seu provedor de serviços de armazenamento de nuvem. Saudação de uso **configurações gerais** folha no dispositivo toomodify Olá tempo as configurações do dispositivo.

![Descrição do dispositivo em configurações gerais](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 Selecione seu fuso horário na lista suspensa de saudação. Você pode especificar os servidores de protocolo NTP (Network Time) tootwo:

 - **O servidor NTP primário** -configuração Olá é necessário e é especificado quando você usa o Windows PowerShell para StorSimple tooconfigure seu dispositivo. Você pode especificar o padrão de saudação do Windows Server **time.windows.com** como o servidor NTP. Você pode exibir hello principal configuração do servidor NTP por meio de saudação portal do Azure, mas você deve usar toochange de interface do Windows PowerShell Olá-lo. Saudação de uso `Set-HcsNTPClientServerAddress` cmdlet toomodify Olá principal o servidor NTP do dispositivo. Para obter mais informações, acesse toosynxtax cmdlet [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx).

- **O servidor NTP secundário** -Olá configuração é opcional. Você pode usar o hello portal tooconfigure um servidor NTP secundário.

Ao configurar o servidor NTP hello, certifique-se de que sua rede permite toopass de tráfego NTP saudação do toohello seu data center da Internet. Ao especificar um servidor NTP público, você deve garantir que seus firewalls de rede e outros dispositivos de segurança serão configurado tooallow NTP tráfego tootravel tooand de saudação fora da rede. Se o tráfego NTP bidirecional não for permitido, será preciso usar um servidor NTP interno (um controlador de domínio do Windows oferece essa função). Se o dispositivo não é possível sincronizar o tempo, pode não ser capaz de toocommunicate com seu provedor de armazenamento de nuvem.

toosee uma lista de servidores NTP públicos, vá toohello [NTP servidores Web](http://support.ntp.org/bin/view/Servers/WebHome).

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>O que acontece se o dispositivo Olá é implantado em um fuso horário diferente?

Se dispositivo Olá é implantado em um fuso horário diferente, fuso horário dispositivo hello serão alterados. Considerando que todas as políticas de backup Olá usam o fuso horário dispositivo hello, políticas de backup Olá ajustará automaticamente conforme Olá novo fuso. Nenhuma intervenção do usuário é necessária.

## <a name="modify-dns-settings"></a>Modificar as configurações de DNS

Um servidor DNS é usado quando o dispositivo tenta toocommunicate com seu provedor de serviços de armazenamento de nuvem. Saudação de uso **as configurações de rede** folha no seu dispositivo tooview e modificar as configurações de DNS de saudação configurada. 

![Configurações de DNS nas Configurações de rede](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

Para alta disponibilidade, você está tooconfigure necessário ambos Olá primário e Olá servidores DNS secundários durante a implantação de dispositivo inicial hello.

**Servidor DNS primário** -usar saudação do Windows PowerShell para StorSimple toofirst especifique o servidor DNS primário de saudação durante a instalação inicial do hello. Você pode reconfigurar o servidor DNS primário do hello somente por meio da interface do Windows PowerShell Olá. Saudação de uso `Set-HcsDNSClientServerAddress` cmdlet toomodify Olá servidor DNS primário do seu dispositivo. Para obter mais informações, visite toosynxtax [Set-HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.

**Servidor DNS secundário** -toomodify Olá servidor DNS secundário, use Olá `Set-HcsDNSClientServerAddress` cmdlet na interface do Windows PowerShell de saudação do dispositivo hello ou **as configurações de rede** folha do seu dispositivo StorSimple no hello Azure Portal.

toomodify Olá servidor DNS secundário no portal do Azure, execute Olá etapas a seguir.

1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Na lista de saudação de dispositivos, selecione e clique em seu dispositivo.

2. Em Olá **configurações** folha, ir muito**configurações do dispositivo > rede**. Isso abre a saudação **as configurações de rede** folha. Clique no bloco **Configurações de DNS**. Modificar Olá secundário IP endereço do servidor DNS.

    ![Modifique o endereço IP do servidor DNS secundário](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. Na barra de comandos de saudação, clique em **salvar** e quando solicitado a confirmar, clique em **Okey**.

    ![Salvar e confirmar as alterações](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>Modificar as interfaces de rede

O dispositivo tem seis interfaces de rede, quatro delas são de 1 GbE e duas são de 10 GbE. Essas interfaces são rotuladas como DATA 0 – DATA 5. DATA 0, DATA 1, DATA 4 e DATA 5 são de 1 GbE, enquanto DATA 2 e DATA 3 são interfaces de rede de 10 GbE.

Saudação de uso **as configurações de rede** folha tooconfigure cada de saudação interfaces toobe usado.

![Configurar adaptadores de rede por meio de Configurações de rede](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure alta disponibilidade, é recomendável que você tenha pelo menos duas interfaces de iSCSI e duas interfaces de nuvem habilitada em seu dispositivo. É recomendável, mas não obrigatório, que as interfaces não utilizadas sejam desabilitadas.

Para cada interface de rede, Olá parâmetros a seguir é exibida:

* **Velocidade** – Não é um parâmetro configurável pelo usuário. DATA 0, DATA 1, DATA 4 e DATA 5 são sempre de 1 GbE, enquanto DATA 2 e DATA 3 são interfaces de 10 GbE.
  
  > [!NOTE]
  > Velocidade e duplex são sempre negociados automaticamente. Não há suporte para quadros Jumbo.
  
* **Estado da interface** – Uma interface pode ser habilitada ou desabilitada. Se habilitada, o dispositivo Olá tentará toouse interface de saudação. Recomendamos que somente essas interfaces de rede conectados toohello e usados esteja habilitado. Desabilite qualquer interface que não estiver em uso.
* **Tipo de interface** – este parâmetro permite que você tooisolate o tráfego iSCSI do tráfego de armazenamento de nuvem. Esse parâmetro pode ser um dos seguintes hello:
  
  * **Habilitada para nuvem** – quando habilitada, dispositivo Olá usará essa interface toocommunicate com nuvem hello.
  * **iSCSI habilitado** – quando habilitado, o dispositivo de Olá usará essa interface toocommunicate com host iSCSI de saudação.
    
    É recomendável isolar o tráfego iSCSI do tráfego do armazenamento em nuvem. Também observe se o host está dentro de saudação mesma sub-rede que o dispositivo, você não precisa tooassign um gateway. No entanto, se o host em uma sub-rede diferente de seu dispositivo, você precisará tooassign um gateway.
* **Endereço IP** – quando você configurar qualquer uma das interfaces de rede hello, você deve configurar um IP virtual (VIP). Ele poderá ser IPv4 ou IPv6 ou ambos. Olá IPv4 e famílias de endereço IPv6 têm suporte para interfaces de rede hello. Ao usar o IPv4, especifique um endereço IP de 32 bits (*xxx.xxx.xxx.xxx*) em notação de ponto decimal. Ao usar o IPv6, basta fornecer um prefixo de quatro dígitos, e um endereço de 128 bits será gerado automaticamente para a interface de rede do dispositivo com base nesse prefixo.
* **Subrede** – isso se refere a máscara de sub-rede toohello e é configurado por meio da interface do Windows PowerShell hello.
* **Gateway** – este é o gateway padrão de saudação que deve ser usado por esta interface quando ele tenta toocommunicate conosco que não estão no hello mesmo espaço de endereço IP (sub-rede). Olá gateway padrão deve estar no hello mesmo espaço de endereço (sub-rede) como o endereço IP da interface hello, conforme determinado pela máscara de sub-rede de saudação.
* **Endereço IP fixo** – esse campo está disponível somente ao configurar Olá DATA 0 interface. Para operações como atualizações ou solução de problemas de dispositivo de saudação, talvez seja necessário tooconnect toohello controlador do dispositivo diretamente. Olá, endereço IP fixo pode ser usado tooaccess Olá ativo e o controlador passivo de saudação em seu dispositivo.

> [!NOTE]
> * tooensure a operação correta, verifique se a velocidade da interface hello e duplex no comutador hello que cada interface de dispositivo está conectado ao. As interfaces de comutador devem negociar com Gigabit Ethernet (1000 Mbps) ou serem configuradas para ela e devem ser full duplex. Interfaces que operam em velocidades menores ou em half-duplex causarão problemas de desempenho.
> * toominimize interrupções e tempo de inatividade, recomendamos que você habilite a opção portfast em cada comutador hello portas Olá interface de rede iSCSI do seu dispositivo irá se conectar. Isso irá garantir a conectividade de rede pode ser estabelecida rapidamente no caso de saudação de um failover.

### <a name="configure-data-0"></a>Configurar DATA 0

DATA 0 é habilitada para nuvem por padrão. Ao configurar o DATA 0, também é necessário tooconfigure dois endereços IP fixos, um para cada controlador. Esses endereços IP fixos podem ser controladores de dispositivo Olá tooaccess usadas diretamente e são úteis quando você instala atualizações no dispositivo de saudação ou quando você acessa controladores Olá para finalidade de saudação de solução de problemas.

Você pode reconfigurar Olá fixa controladores IP por meio da folha de configurações de 0 dados hello.

![Configurar adaptador de rede – DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> Olá endereços IP para o controlador de saudação fixos são usados para atender dispositivo de toohello atualizações hello. Portanto, Olá IPs fixo deve ser roteáveis e capazes de tooconnect toohello da Internet.

### <a name="configure-data-1---data-5"></a>Configurar DATA 1 – DATA 5

Para dados de 1 - interfaces de rede 5 de dados, você pode configurar todas as configurações de rede Olá conforme Olá captura de tela a seguir:

![Configurar os adaptadores de rede DATA 1 – DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>Alternar ou reatribuir IPs

No momento, se qualquer interface de rede no controlador de saudação é atribuído um VIP que está em uso (por Olá mesmo dispositivo ou outro dispositivo de rede Olá), e controlador Olá irão falhar. Se você trocar ou reatribuir VIPs para um adaptador de rede do dispositivo, será necessário seguir um procedimento adequado como se você pudesse criar uma situação de IP duplicada.

Executar Olá tooswap as etapas a seguir ou reatribuir Olá VIPs para qualquer uma das interfaces de rede hello:

#### <a name="tooreassign-ips"></a>tooreassign IPs

1. Endereço IP hello clara para ambas as interfaces.
2. Depois de endereços IP de saudação são limpas, atribua novos endereços IP hello toohello respectivas interfaces.

## <a name="next-steps"></a>Próximas etapas

* Saiba como muito[configurar o MPIO para seu dispositivo StorSimple](storsimple-8000-configure-mpio-windows-server.md).
* Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

