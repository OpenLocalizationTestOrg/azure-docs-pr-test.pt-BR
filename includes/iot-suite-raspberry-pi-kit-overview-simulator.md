## <a name="overview"></a>Visão geral

Neste tutorial, você deve concluir Olá etapas a seguir:

- Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure. Esta etapa implanta e configura automaticamente vários serviços do Azure.
- Configure toocommunicate seu dispositivo com o computador e a solução de monitoramento remoto hello.
- Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria simulada que você pode exibir no painel de solução de saudação.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.

> [!NOTE]
> Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].

### <a name="required-software"></a>Software necessário

Você precisa cliente SSH no seu tooenable computador desktop você tooremotely acesso Olá linha de comando em Olá framboesa Pi.

- O Windows não inclui um cliente SSH. Recomendamos o uso de [PuTTY](http://www.putty.org/).
- A maioria das distribuições do Linux e Mac OS incluem o utilitário SSH de linha de comando do hello. Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

### <a name="required-hardware"></a>Requisitos de hardware

Um computador desktop tooenable você tooconnect remotamente toohello linha de comando em Olá framboesa Pi.

[Microsoft IoT Starter Kit para Raspberry Pi 3][lnk-starter-kits] ou componentes equivalentes. Este tutorial usa Olá itens a seguir do kit de saudação:

- Raspberry Pi 3
- Cartão MicroSD (com NOOBS)
- Um cabo USB Mini
- Um cabo Ethernet

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/