---
title: "a configuração do dispositivo StorSimple aaaModify Olá | Microsoft Docs"
description: "Descreve como toouse Olá tooreconfigure do serviço StorSimple Manager um dispositivo StorSimple que já tenha sido implantado."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 10a54c191260bf1baba58d28cdbfa0ed72217f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomodify-your-storsimple-device-configuration"></a>Usar toomodify de serviço do StorSimple Manager Olá a configuração do dispositivo StorSimple
## <a name="overview"></a>Visão geral
Olá portal clássico do Azure **configurar** página contém todos os parâmetros de dispositivo de saudação que você pode reconfigurar em um dispositivo StorSimple que é gerenciado por um serviço StorSimple Manager. Este tutorial explica como você pode usar o hello **configurar** Olá tooperform de página tarefas de nível de dispositivo a seguir:

* Modificar as configurações de dispositivo 
* Modificar as configurações de tempo 
* Modificar as configurações de DNS 
* Modificar as interfaces de rede
* Alternar ou reatribuir IPs

## <a name="modify-device-settings"></a>Modificar as configurações de dispositivo
configurações de saudação do dispositivo incluem nome amigável de saudação do dispositivo hello e descrição do dispositivo hello.

> [!NOTE] 
> Não é possível modificar o nome de dispositivo de saudação no hello portal clássico do Azure. Não há suporte para renomear o dispositivo hello.

Um dispositivo StorSimple que é conectado toohello serviço StorSimple Manager é atribuído um nome padrão. Olá geralmente reflete Olá o número de série do dispositivo hello. Por exemplo, um nome de dispositivo padrão que é de 15 caracteres, como 8600-SHX0991003G44HT indica a seguir hello:

* **8600** – indica o modelo de dispositivo hello.
* **SHX** – site de produção de hello indica.
* **0991003** - Indica um produto específico.
* **G44HT**- Olá últimos 5 dígitos são incrementados toocreate números de série exclusivos. Isso pode não ser um conjunto sequencial.

É possível especificar uma descrição de dispositivo. Uma descrição do dispositivo geralmente ajuda a identificar o proprietário hello e a localização física de saudação do dispositivo hello. campo de descrição de saudação deve conter menos de 256 caracteres.

## <a name="modify-time-settings"></a>Modificar as configurações de tempo
O dispositivo deve sincronizar o tempo em ordem tooauthenticate com seu provedor de serviços de armazenamento de nuvem. Selecione seu fuso horário na lista suspensa de saudação e especificar os servidores de protocolo NTP (Network Time) tootwo. o servidor NTP primário Olá é necessário e é especificado quando você usa o Windows PowerShell para StorSimple tooconfigure seu dispositivo. Você pode especificar o padrão de saudação do Windows Server **time.windows.com** como o servidor NTP. Você pode exibir hello principal configuração do servidor NTP por meio de saudação portal clássico do Azure, mas você deve usar toochange de interface do Windows PowerShell Olá-lo.

configuração do servidor NTP secundária Olá é opcional. Você pode usar tooconfigure portal clássico Olá um servidor NTP secundário. 

Ao configurar o servidor NTP hello, certifique-se de que sua rede permite toopass de tráfego NTP saudação do toohello seu data center da Internet. Ao especificar um servidor NTP público, você deve garantir que seus firewalls de rede e outros dispositivos de segurança serão configurado tooallow NTP tráfego tootravel tooand de saudação fora da rede. Se o tráfego NTP bidirecional não for permitido, será preciso usar um servidor NTP interno (um controlador de domínio do Windows oferece essa função). Se o dispositivo não é possível sincronizar o tempo, pode não ser capaz de toocommunicate com seu provedor de armazenamento de nuvem.

toosee uma lista de servidores NTP públicos, vá toohello [NTP servidores Web](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>O que acontece se o dispositivo Olá é implantado em um fuso horário diferente?
Se dispositivo Olá é implantado em um fuso horário diferente, fuso horário dispositivo hello serão alterados. Considerando que todas as políticas de backup Olá usam o fuso horário dispositivo hello, políticas de backup Olá ajustará automaticamente conforme Olá novo fuso. Nenhuma intervenção do usuário é necessária.

## <a name="modify-dns-settings"></a>Modificar as configurações de DNS
Um servidor DNS é usado quando o dispositivo tenta toocommunicate com seu provedor de serviços de armazenamento de nuvem. Para alta disponibilidade, você está tooconfigure necessário ambos Olá primário e Olá servidores DNS secundários durante a implantação de dispositivo inicial hello. tooreconfigure Olá servidor DNS primário você precisará interface do toouse saudação do Windows PowerShell em seu dispositivo StorSimple.

toomodify Olá servidor DNS secundário, você pode usar o hello portal clássico do Azure.

## <a name="modify-network-interfaces"></a>Modificar as interfaces de rede
O dispositivo tem seis interfaces de rede, quatro delas são de 1 GbE e duas são de 10 GbE. Essas interfaces são rotuladas como DATA 0 – DATA 5. DATA 0, DATA 1, DATA 4 e DATA 5 são de 1 GbE, enquanto DATA 2 e DATA 3 são interfaces de rede de 10 GbE.

Configurar **as configurações de Interface de rede** para cada Olá interfaces toobe usado. tooensure alta disponibilidade, é recomendável que você tenha pelo menos duas interfaces de iSCSI e duas interfaces de nuvem habilitada em seu dispositivo. É recomendável, mas não obrigatório, que as interfaces não utilizadas sejam desabilitadas.

Quando você configurar qualquer uma das interfaces de rede hello, você deve configurar um IP virtual (VIP).

DATA 0 é habilitada para nuvem por padrão. Ao configurar o DATA 0, também é necessário tooconfigure dois endereços IP fixos, um para cada controlador. Esses endereços IP fixos podem ser controladores de dispositivo Olá tooaccess usadas diretamente e são úteis quando você instala atualizações no dispositivo de saudação ou quando você acessa controladores Olá para finalidade de saudação de solução de problemas.

StorSimple 8000 Series atualização 1, métrica de roteamento de saudação de DATA 0 é definida toohello mais baixo; Portanto, se o dispositivo está executando StorSimple 8000 Series atualização 1, todo o tráfego de nuvem hello será roteado por meio de dados 0. Anote isso se houver mais de uma interface de rede habilitada para nuvem em seu dispositivo StorSimple.

> [!NOTE]
> Olá endereços IP para o controlador de saudação fixos são usados para atender dispositivo de toohello atualizações hello. Portanto, Olá IPs fixo deve ser roteáveis e capazes de tooconnect toohello da Internet.
> 
> 

Para cada interface de rede, Olá parâmetros a seguir é exibida:

* **Velocidade** – Não é um parâmetro configurável pelo usuário. DATA 0, DATA 1, DATA 4 e DATA 5 são sempre de 1 GbE, enquanto DATA 2 e DATA 3 são interfaces de 10 GbE.
  
  > [!NOTE]
  > Velocidade e duplex são sempre negociados automaticamente. Não há suporte para quadros Jumbo.
  > 
  > 
* **Estado da interface** – Uma interface pode ser habilitada ou desabilitada. Se habilitada, o dispositivo Olá tentará toouse interface de saudação. Recomendamos que somente essas interfaces de rede conectados toohello e usados esteja habilitado. Desabilite qualquer interface que não estiver em uso.
* **Tipo de interface** – este parâmetro permite que você tooisolate o tráfego iSCSI do tráfego de armazenamento de nuvem. Esse parâmetro pode ser um dos seguintes hello:
  
  * **Habilitada para nuvem** – quando habilitada, dispositivo Olá usará essa interface toocommunicate com nuvem hello.
  * **iSCSI habilitado** – quando habilitado, o dispositivo de Olá usará essa interface toocommunicate com host iSCSI de saudação.
    
    É recomendável isolar o tráfego iSCSI do tráfego do armazenamento em nuvem. Também observe se o host está dentro de saudação mesma sub-rede que o dispositivo, você não precisa tooassign um gateway. No entanto, se o host em uma sub-rede diferente de seu dispositivo, você precisará tooassign um gateway.
* **Endereço IP** – Pode ser IPv4, IPv6 ou ambos. Olá IPv4 e famílias de endereço IPv6 têm suporte para interfaces de rede hello. Ao usar o IPv4, especifique um endereço IP de 32 bits (*xxx.xxx.xxx.xxx*) em notação de ponto decimal. Ao usar o IPv6, basta fornecer um prefixo de quatro dígitos, e um endereço de 128 bits será gerado automaticamente para a interface de rede do dispositivo com base nesse prefixo.
* **Subrede** – isso se refere a máscara de sub-rede toohello e é configurado por meio da interface do Windows PowerShell hello.
* **Gateway** – este é o gateway padrão de saudação que deve ser usado por esta interface quando ele tenta toocommunicate conosco que não estão no hello mesmo espaço de endereço IP (sub-rede). Olá gateway padrão deve estar no hello mesmo espaço de endereço (sub-rede) como o endereço IP da interface hello, conforme determinado pela máscara de sub-rede de saudação.
* **Endereço IP fixo** – esse campo está disponível somente ao configurar Olá DATA 0 interface. Para operações como atualizações ou solução de problemas de dispositivo de saudação, talvez seja necessário tooconnect toohello controlador do dispositivo diretamente. Olá, endereço IP fixo pode ser usado tooaccess Olá ativo e o controlador passivo de saudação em seu dispositivo.

Você pode reconfigurar o controlador 0 e 1 por meio de saudação portal clássico do Azure.

> [!NOTE]
> * tooensure a operação correta, verifique se a velocidade da interface hello e duplex no comutador hello que cada interface de dispositivo está conectado ao. As interfaces de comutador devem negociar com Gigabit Ethernet (1000 Mbps) ou serem configuradas para ela e devem ser full duplex. Interfaces que operam em velocidades menores ou em half-duplex causarão problemas de desempenho.
> * toominimize interrupções e tempo de inatividade, recomendamos que você habilite a opção portfast em cada comutador hello portas Olá interface de rede iSCSI do seu dispositivo irá se conectar. Isso irá garantir a conectividade de rede pode ser estabelecida rapidamente no caso de saudação de um failover.
> 
> 

## <a name="swap-or-reassign-ips"></a>Alternar ou reatribuir IPs
No momento, se qualquer interface de rede no controlador de saudação é atribuído um VIP que está em uso (por Olá mesmo dispositivo ou outro dispositivo de rede Olá), e controlador Olá irão falhar. Portanto, você tem procedimento adequado do toofollow Olá se permutar VIPs para a interface de rede do dispositivo hello, porque você criará uma situação de IP duplicado.

Executar Olá tooswap as etapas a seguir ou reatribuir Olá VIPs para qualquer uma das interfaces de rede hello:

#### <a name="tooreassign-ips"></a>tooreassign IPs
1. Endereço IP hello clara para ambas as interfaces.
2. Depois de endereços IP de saudação são limpas, atribua novos endereços IP hello toohello respectivas interfaces.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[configurar o MPIO para seu dispositivo StorSimple](storsimple-configure-mpio-windows-server.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

