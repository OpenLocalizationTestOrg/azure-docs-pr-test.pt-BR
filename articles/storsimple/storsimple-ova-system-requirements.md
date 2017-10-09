---
title: requisitos de sistema do Azure StorSimple Virtual Array aaaMicrosoft | Microsoft Docs
description: "Saiba mais sobre os requisitos de software e rede Olá para sua matriz Virtual StorSimple"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>Requisitos do sistema da StorSimple Virtual Array
## <a name="overview"></a>Visão geral
Este artigo descreve os requisitos de sistema importantes Olá para sua matriz do Microsoft Azure StorSimple Virtual e Olá para clientes de armazenamento ao acessar a matriz de saudação. Recomendamos que você analise Olá informações cuidadosamente antes de implantar o sistema StorSimple e, em seguida, voltar tooit conforme necessário durante a implantação e operação subsequente.

requisitos do sistema Olá incluem:

* **Requisitos de software para clientes de armazenamento** -descreve Olá suporte para plataformas de virtualização, navegadores da web, os clientes iniciadores iSCSI, SMB, os requisitos mínimos de dispositivo virtual e quaisquer requisitos adicionais para esses sistemas operacionais.
* **Requisitos de rede para o dispositivo StorSimple Olá** -fornece informações sobre portas de saudação que toobe necessidade aberto no tooallow seu firewall para tráfego iSCSI, nuvem ou gerenciamento.

requisitos do sistema StorSimple Olá informações publicadas neste artigo se aplica a tooStorSimple matrizes Virtual.

* Para dispositivos da 8000 série, vá muito[requisitos do sistema para o dispositivo da série StorSimple 8000](storsimple-system-requirements.md).
* Para dispositivos da 7000 série, vá muito[requisitos do sistema para o dispositivo da série StorSimple 7000 5000](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements).

## <a name="software-requirements"></a>Requisitos de software
requisitos de software Olá incluem informações de saudação em navegadores da web de saudação com suporte, versões SMB, plataformas de virtualização e requisitos de mínimos de dispositivo virtual Olá.

### <a name="supported-virtualization-platforms"></a>Plataformas de virtualização com suporte
| **Hipervisor** | **Versão** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 e posterior |
| VMware ESXi |5.5 e posterior |

### <a name="virtual-device-requirements"></a>Requisitos de dispositivo virtual
| **Componente** | **Requisito** |
| --- | --- |
| Número mínimo de processadores virtuais (núcleos) |4 |
| Mínimo de memória (RAM) |8 GB <br> Para um servidor de arquivos, 8 GB para menos de 2 milhões de arquivos e 16 GB para 2 a 4 milhões de arquivos|
| Espaço em disco<sup>1</sup> |Disco do sistema operacional - 80 GB  <br></br>Disco de dados - 500 GB too8 TB |
| Número mínimo de interface(s) de rede |1 |
| Largura de banda mínima da Internet<sup>2</sup> |5 Mbps |

<sup>1</sup> - Com provisionamento dinâmico

<sup>2</sup> -requisitos de rede podem variar dependendo da taxa de alteração de dados diária hello. Por exemplo, se um dispositivo precisa tooback 10 GB ou mais alterações durante um dia, em seguida, hello backup diário sobre uma conexão Mbps 5 pode levar até too4.25 horas (se os dados de saudação não podem ser compactados ou com eliminação de duplicação).

### <a name="supported-web-browsers"></a>Navegadores da Web com suporte
| **Componente** | **Versão** | **Requisitos/observações adicionais** |
| --- | --- | --- |
| Microsoft Edge |Última versão | |
| Internet Explorer |Última versão |Testado com o Internet Explorer 11 |
| Google Chrome |Última versão |Testado com o Chrome 46 |

### <a name="supported-storage-clients"></a>Clientes de armazenamento com suporte
Olá, requisitos de software a seguir é para os iniciadores iSCSI Olá que acessam sua matriz Virtual do StorSimple (configurado como um servidor iSCSI).

| **Sistemas operacionais com suporte** | **Versão necessária** | **Requisitos/observações adicionais** |
| --- | --- | --- |
| Windows Server |2008R2 SP1, 2012, 2012R2 |O StorSimple pode criar volumes com provisionamento dinâmico e provisionamento completo. Ele não pode criar volumes com provisionamento parcial. Os volumes iSCSI do StorSimple têm suporte apenas em:  <ul><li>Volumes simples em discos básicos do Windows.</li><li>Windows NTFS para formatar um volume.</li> |

Olá, requisitos de software a seguir é para Olá clientes SMB que acessam sua matriz Virtual do StorSimple (configurado como um servidor de arquivos).

| **Versão do SMB** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> Não copie ou armazenar arquivos protegidos pelo servidor de arquivos do Windows Encrypting File System (EFS) toohello matriz Virtual StorSimple; Isso resultará em uma configuração sem suporte. 
> 

### <a name="supported-storage-format"></a>Formato de armazenamento com suporte
Olá armazenamento de blob de blocos do Azure tem suporte. Blobs de página não têm suporte. Para obter mais informações [sobre blobs de blocos e blobs de página](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).

## <a name="networking-requirements"></a>Requisitos de rede
Olá tabela a seguir lista portas Olá que precisam toobe aberto no tooallow seu firewall para iSCSI, SMB, nuvem ou tráfego de gerenciamento. Nessa tabela, *na* ou *entrada* refere-se toohello direção na qual a solicitações de cliente recebidas acessar seu dispositivo. *Out* ou *saída* refere-se toohello direção na qual o seu dispositivo StorSimple envia dados externamente, além da implantação Olá: por exemplo, a saída toohello da Internet.

| **Porta No.<sup>1</sup>** | **Entrada ou saída** | **Escopo da porta** | **Obrigatório** | **Observações** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |Saída |WAN |Não |Porta de saída é usada para atualizações de tooretrieve de acesso à Internet. <br></br>proxy da web de saída de saudação é configurável pelo usuário. |
| TCP 443 (HTTPS) |Saída |WAN |Sim |Porta de saída é usada para acessar dados em nuvem hello. <br></br>proxy da web de saída de saudação é configurável pelo usuário. |
| UDP 53 (DNS) |Saída |WAN |Em alguns casos; consulte as observações. |Esta porta só será necessária se você estiver usando um servidor DNS baseado na Internet. <br></br> Observe que, caso esteja implantando um servidor de arquivos, recomendamos usar o servidor DNS local. |
| UDP 123 (NTP) |Saída |WAN |Em alguns casos; consulte as observações. |Esta porta é necessária apenas se você estiver usando um servidor NTP baseado na Internet.<br></br> Observe que, caso esteja implantando um servidor de arquivos, recomendamos sincronizar a hora com os controladores de domínio do Active Directory. |
| TCP 80 (HTTP) |No |LAN |Sim |Isso é hello porta de entrada para a interface de usuário local no dispositivo do StorSimple Olá para gerenciamento local. <br></br> Observe que acessar Olá UI local via HTTP será automaticamente redirecionada tooHTTPS. |
| TCP 443 (HTTPS) |No |LAN |Sim |Isso é hello porta de entrada para a interface de usuário local no dispositivo do StorSimple Olá para gerenciamento local. |
| TCP 3260 (iSCSI) |No |LAN |Não |Esta porta é usada tooaccess dados por iSCSI. |

<sup>1</sup> toobe aberto em não precisa de nenhuma porta de entrada hello Internet pública.

> [!IMPORTANT]
> Verifique se o firewall Olá não modificar ou descriptografar qualquer tráfego SSL entre o dispositivo StorSimple hello e o Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Padrões de URL para regras de firewall
Os administradores de rede geralmente podem configurar regras com base em Olá Olá de toofilter de padrões de URL de entrada e o tráfego de saída de hello avançadas do firewall. Sua matriz virtual e hello serviço do Gerenciador de dispositivos de StorSimple dependem de outros aplicativos da Microsoft, como o Azure Service Bus, controle de acesso do Azure Active Directory, contas de armazenamento e servidores do Microsoft Update. padrões de URL Olá associados a esses aplicativos podem ser usados tooconfigure as regras de firewall. É importante toounderstand que podem alterar os padrões de URL Olá associados a esses aplicativos. Isso por sua vez exigem Olá toomonitor de administrador de rede e atualizar regras de firewall para o StorSimple como e quando necessário. 

É recomendável que você defina suas regras de firewall para tráfego de saída, com base nos endereços IP fixos do StorSimple e, na maioria dos casos, de modo flexível. No entanto, você pode usar informações de saudação abaixo tooset avançadas de regras de firewall que são ambientes seguros toocreate necessários.

> [!NOTE]
> 
> * dispositivo de saudação (origem) IPs deve sempre ser definido interfaces de rede habilitados para a nuvem de saudação do tooall. 
> * destino de saudação IPs deve ser definido muito[intervalos IP do datacenter do Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

| Padrão de URL | Componente/funcionalidade |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Serviço do Gerenciador de Dispositivos StorSimple<br>Access Control Service<br>Barramento de Serviço do Azure |
| `http://*.backup.windowsazure.com` |Registro de dispositivos |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revogação de certificado |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Contas de armazenamento e monitoramento do Azure |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores do Microsoft Update<br> |
| `http://*.deploy.akamaitechnologies.com` |CDN do Akamai |
| `https://*.partners.extranet.microsoft.com/*` |Pacote de suporte |
| `http://*.data.microsoft.com ` |O serviço de telemetria no Windows, consulte Olá [atualização para a experiência do cliente e telemetria de diagnóstico](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>Próxima etapa
* [Preparar toodeploy portal Olá sua matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md)

