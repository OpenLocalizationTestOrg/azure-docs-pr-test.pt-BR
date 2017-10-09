---
title: "aaaAzure solução de problemas de criptografia de disco | Microsoft Docs"
description: "Este artigo fornece dicas de solução de problemas para o Microsoft Azure Disk Encryption para VMs de IaaS do Windows e Linux."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Guia de resolução de problemas do Azure Disk Encryption

Este guia é para profissionais de TI (tecnologia) de informações, informações de analistas de segurança, e os administradores de nuvem cujas organizações estão usando a criptografia de disco do Azure e precisam de criptografia de disco orientação tootroubleshoot relacionados a problemas.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Solução de problemas de criptografia de disco do SO Linux

Criptografia de disco do sistema operacional Linux deve desmontar Olá SO unidade anterior toorunning-lo por meio do processo de criptografia de disco cheio hello.   Caso contrário, uma mensagem de erro "Falha toounmount após..." mensagem de erro é provavelmente toooccur.

Isso é muito provável quando a criptografia de disco do SO for tentada em um ambiente de VM de destino modificado ou alterado a partir da imagem da galeria de estoque com suporte.  Exemplos de desvios da imagem de saudação com suporte, que pode interferir na unidade de saudação SO da extensão Olá capacidade toounmount incluem:
- Imagens personalizadas que não correspondem mais a um sistema de arquivos com suporte e/ou esquema de particionamento.
- Imagens personalizadas com aplicativos como antivírus, Docker, SAP, MongoDB ou Apache Cassandra em execução no tooencryption anterior do sistema operacional hello.  Esses aplicativos são difíceis tooterminate e quando eles mantêm a unidade de toohello OS de identificadores de arquivos abertos, unidade de saudação não pode ser desmontada, causando a falha.
- Os scripts personalizados que são executados em Fechar etapa de criptografia toohello proximidade pode interferir e causar a falha de tempo. Isso pode acontecer quando um modelo do Gerenciador de recursos define tooexecute de várias extensões ao mesmo tempo, ou quando uma extensão de script personalizado ou outra ação é executar simultaneamente toodisk criptografia.   Serialização e isolando essas etapas podem resolver o problema de saudação.
- Quando SELinux não tiver sido desabilitado tooenabling anterior criptografia, Olá desmontar a etapa falhar.  O SELinux pode ser novamente habilitado após a conclusão da criptografia.
- Quando o disco Olá SO está usando um esquema de LVM (embora suporte limitado de disco de dados LVM estiver disponível, o disco de SO LVM não é)
- Quando os requisitos mínimos de memória não são atendidos (7 GB é sugerido para criptografia de disco do SO)
- Quando as unidades de dados foram montadas recursivamente no diretório /mnt/ ou outro (por exemplo, /mnt/data1, /mnt/data2, /data3 + /data3/data4, etc.)
- Quando outros [pré-requisitos](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) do Azure Disk Encryption para Linux não forem atendidos

## <a name="unable-tooencrypt"></a>Não é possível tooencrypt

Em alguns casos, a criptografia de disco Linux Olá aparece toobe preso em "Criptografia de disco SO iniciada" e SSH está desabilitada. Esse processo pode levar entre toocomplete 3-16 horas em uma imagem da Galeria de estoque.  Se os discos de dados do multi-TB tamanho são adicionados, o processo de saudação pode levar dias. Olá sequência de criptografia de disco do sistema operacional Linux desmonta a unidade de saudação SO temporariamente e realiza a criptografia no bloco por bloco de disco do sistema operacional inteiro hello, antes de remontá-lo em seu estado criptografado.   Ao contrário de criptografia de disco do Azure no Windows, criptografia de disco do Linux não permitir uso simultâneo de saudação VM enquanto Olá criptografia está em andamento.  características de desempenho de saudação de saudação VM, incluindo tamanho de saudação do disco hello e se a conta de armazenamento Olá é apoiada por armazenamento (SSD) padrão ou premium, podem influenciar bastante Olá tempo necessário toocomplete criptografia.

status de toocheck, campo de ProgressMessage Olá retornado de saudação [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) comando pode ser controlado.   Enquanto unidade Olá sistema operacional está sendo criptografada, Olá VM entra em um estado de manutenção e SSH também é desabilitado tooprevent qualquer processo contínuo de toohello de interrupção.  EncryptionInProgress será relatado para a maioria de saudação do tempo de saudação enquanto a criptografia estiver em andamento, seguido de várias horas mais tarde com uma mensagem de VMRestartPending solicitando toorestart Olá VM.  Por exemplo:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Uma vez solicitado tooreboot Olá VM e, depois de reiniciar Olá VM e dando 2 a 3 minutos para reinicialização hello e etapas finais toobe executada no destino hello, mensagem de saudação do status indicará que a criptografia foi concluída por último.   Quando essa mensagem estiver disponível, unidade do sistema operacional Olá criptografado é esperado toobe pronto para uso em Olá VM toobe utilizável novamente.

Em casos onde essa sequência não foi Vista, ou se as informações de inicialização, mensagem de progresso ou outros indicadores de erro informar que a criptografia de sistema operacional falhou no meio hello desse processo (por exemplo, se você estiver vendo o erro de "Falha toounmount" hello descrito neste guia), é recomendável instantâneo de backup toohello toorestore Olá VM ou backup feito tooencryption imediatamente anterior.  Próxima tentativa de toohello anterior, é sugerida toore-avaliar características de saudação do hello VM e certifique-se de que todos os pré-requisitos forem atendidos.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Solução de problemas do Azure Disk Encryption por trás de um firewall
Quando conectividade é restrito por capacidade de Olá um firewall, o requisito de proxy ou configurações de grupo (NSG) de segurança de rede, de saudação extensão tooperform necessário tarefas pode ser interrompidas.   Isso pode resultar em mensagens de status como "Status da extensão não está disponível em Olá VM" e em cenários esperados falhando toofinish.  Olá próximas seções tem alguns problemas comuns de firewall que você pode investigar.

### <a name="network-security-groups"></a>Grupos de segurança de rede
As configurações de grupo de segurança de rede aplicadas ainda devem permitir a configuração de rede do hello ponto de extremidade toomeet Olá documentado [pré-requisitos](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) para criptografia de disco.

### <a name="azure-keyvault-behind-firewall"></a>Azure Keyvault por trás do firewall
Olá VM deve ser capaz de tooaccess Cofre de chaves. Consulte tooguidance na falha do access tookey por trás de um firewall que é mantida pela Olá [Cofre de chaves](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) equipe.

### <a name="linux-package-management-behind-firewall"></a>Gerenciamento de pacotes Linux por trás do firewall
Em tempo de execução, a criptografia de disco do Azure para Linux depende pacote gerenciamento tooinstall necessário componentes de pré-requisito tooenabling anteriores a criptografia do sistema da distribuição de destino Olá.  Se as configurações de firewall impedir Olá VM toodownload capaz e instalar esses componentes, falhas subsequentes são esperadas.    etapas de saudação tooconfigure que isso pode variar para distribuição.  No Red Hat, quando um proxy é necessário, é vital garantir que o subscription-manager e o yum estejam configurados corretamente.  Consulte [este](https://access.redhat.com/solutions/189533) artigo de suporte do Red Hat sobre esse tópico.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Solução de problemas de Server Core do Windows Server 2016

No Server Core do Windows Server 2016, o componente de bdehdcfg Olá não está disponível por padrão. Esse componente é exigido pelo Azure Disk Encryption.

tooworkaround esse problema, Olá cópia 4 arquivos a seguir de uma pasta de c:\windows\system32 toohello VM do Windows Server 2016 Data Center da imagem do Server Core hello:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Em seguida, execute o comando a seguir de saudação:

```
bdehdcfg.exe -target default
```

Isso criará uma partição de sistema 550MB e, em seguida, após uma reinicialização, você pode usar o Diskpart toocheck Olá volumes e continuar.  

Por exemplo:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu mais sobre alguns problemas comuns na criptografia de disco do Azure e como tootroubleshoot. Para obter mais informações sobre esse serviço e sua capacidade, leia:

- [Aplicar a criptografia de disco na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Criptografar uma Máquina Virtual do Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Criptografia de dados em repouso no Azure](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
