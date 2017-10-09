

## <a name="multi-and-single-instance-vms"></a>VMs de instância única e várias instâncias
Muitos clientes executados na contagem do Azure-crítica que pode agendar quando suas VMs são submetidos a manutenção planejada devido tempo de inatividade toohello – cerca de 15 minutos – que ocorre durante a manutenção. Você pode usar o controle de toohelp de conjuntos de disponibilidade quando máquinas virtuais provisionadas recebem manutenção planejada.

Existem duas possíveis configurações para VMs em execução no Azure. As VMs são configuradas como várias instâncias ou instância única. Se as VMs estiverem em um conjunto de disponibilidade, elas serão configuradas como várias instâncias. Observe que mesmo as VMs únicas podem ser implantadas em um conjunto de disponibilidade, para que elas sejam tratadas como várias instâncias. Se as VMs NÃO estiverem em um conjunto de disponibilidade, elas serão configuradas como instância única.  Para obter detalhes sobre conjuntos de disponibilidade, consulte [Olá de gerenciar a disponibilidade de suas máquinas virtuais do Windows](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Olá de gerenciar a disponibilidade de máquinas virtuais Linux](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Manutenção planejada atualiza a instância de toosingle e várias instâncias VMs acontecerá separadamente. Ao reconfigurar sua única VMs toobe instância (se eles estiverem com várias instâncias) ou toobe várias instâncias (se eles estiverem instância única), você pode controlar quando suas VMs recebem manutenção Olá planejado. Confira [Manutenção planejada de máquinas virtuais Linux do Azure](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [Manutenção planejada de máquinas virtuais Windows do Azure](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter detalhes sobre a manutenção planejada para VMs do Azure.

## <a name="for-multi-instance-configuration"></a>Para configuração de várias instâncias
Você pode selecionar o tempo de saudação manutenção planejada afeta suas VMs que são implantados em uma configuração de conjunto de disponibilidade, removendo essas VMs de conjuntos de disponibilidade.

1. Um email é enviado tooyou sete dias antes Olá planejado manutenção tooyour VMs em uma configuração de várias instâncias. Olá IDs de assinatura e nomes de máquinas virtuais com várias instâncias de Olá afetado são incluídos no corpo de saudação do email hello.
2. Durante os sete dias, você pode escolher suas instâncias de tempo de saudação são atualizadas, removendo suas VMs de várias instâncias dessa região do seu conjunto de disponibilidade. Essa alteração no causas de configuração, uma reinicialização, como Olá Máquina Virtual é movidos de um host físico, direcionado para manutenção, tooanother host físico que não é destinada para manutenção.
3. Você pode remover Olá VM de seu conjunto de disponibilidade no hello portal do Azure.

   1. No portal de saudação, selecione Olá VM tooremove de saudação conjunto de disponibilidade.  

   2. Em **configurações**, clique em **Conjunto de disponibilidade**.

      ![Seleção do conjunto de disponibilidade](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. Disponibilidade de saudação defina o menu suspenso, selecione "Não faz parte de um conjunto de disponibilidade."

      ![Remover do conjunto](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. Na parte superior da saudação, clique em **salvar**. Clique em **Sim** Olá tooacknowledge que essa ação reinicia a VM.

   >[!TIP]
   >Você pode reconfigurar Olá toomulti-instância VM mais tarde, selecionando um dos conjuntos de disponibilidade Olá listado.

4. Removido de conjuntos de disponibilidade de máquinas virtuais são movidos da instância de tooSingle hosts e não são atualizados durante a saudação planejada manutenção tooAvailability definir configurações.
5. Após a conclusão da saudação atualização tooAvailability às VMs de conjunto do (de acordo com tooschedule indicado no email original Olá), você deve adicionar o hello VMs novamente em seus conjuntos de disponibilidade. Tornando-se parte de um conjunto de disponibilidade reconfigura Olá VMs como várias instâncias e resulta em uma reinicialização. Normalmente, depois que todas as atualizações de várias instâncias forem concluídas em todo o ambiente do Azure hello, manutenção de instância única segue.

A remoção de uma VM de um conjunto de disponibilidade também pode ser obtida usando o Azure PowerShell:

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Para configuração de instância única
Você pode selecionar o tempo de saudação manutenção planejada afeta você VMs em uma configuração de instância única, adicionando essas VMs em conjuntos de disponibilidade.

Passo a passo

1. Um email é enviado tooyou sete dias antes Olá planejado tooVMs de manutenção em uma configuração de instância única. Olá IDs de assinatura e nomes de máquinas virtuais de instância única Olá afetado são incluídos no corpo de saudação do email hello.
2. Durante os sete dias, você pode escolher sua instância de tempo de saudação reinicializações, adicionando a disponibilidade do seu tooan VMs de única instância definida na mesma região. Essa alteração no causas de configuração, uma reinicialização, como Olá Máquina Virtual é movidos de um host físico, direcionado para manutenção, tooanother host físico que não é destinada para manutenção.
3. Siga as instruções aqui tooadd existente VMs em conjuntos de disponibilidade usando hello portal do Azure e o Azure PowerShell. (Consulte o exemplo do PowerShell do Azure hello que segue estas etapas.)
4. Depois que essas VMs são reconfigurados como várias instâncias, elas são excluídas de manutenção planejada de saudação tooSingle instância VMs.
5. Após a conclusão da atualização de VM de instância única de saudação (de acordo com tooschedule no email original Olá), poderá retornar Olá VMs toosingle-instância removendo Olá VMs de seus conjuntos de disponibilidade.

Adicionando um tooan VM também conjunto de disponibilidade pode ser obtida usando o Azure PowerShell:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
