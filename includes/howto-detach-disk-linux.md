Quando você não precisa mais um disco de dados é anexado tooa VM (máquina virtual), você pode facilmente desanexá-lo. Ao desanexar um disco de saudação VM, disco Olá não é removido do armazenamento. Se você quiser toouse Olá dados existentes ao disco Olá novamente, você poderá reanexar-toohello mesma VM, ou outro.  

> [!NOTE]
> Uma VM no Azure usa diferentes tipos de discos, um disco de sistema operacional, um disco temporário local e discos de dados opcionais. Para obter detalhes, confira [Sobre discos e VHDs para máquinas virtuais](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Você não pode desanexar um disco do sistema operacional, a menos que você também excluir Olá VM.

## <a name="find-hello-disk"></a>Localizar o disco Olá
Antes de poder desanexar um disco de uma VM é necessário toofind out Olá número LUN, que é um identificador para Olá disco toobe desanexado. toodo que, siga estas etapas:

1. Abra a CLI do Azure e [conectar tooyour assinatura do Azure](../articles/xplat-cli-connect.md). Verifique se você está no modo de Gerenciamento de Serviços do Azure (`azure config mode asm`).
2. Descubra quais discos estão anexado tooyour VM. Olá, exemplo a seguir lista discos para Olá VM denominada `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Observe Olá LUN ou hello **número de unidade lógica** para disco Olá que você deseja toodetach.

## <a name="remove-operating-system-references-toohello-disk"></a>Remover disco do sistema operacional referências toohello
Antes de desanexar o disco de saudação do convidado do Linux hello, você deve garantir que todas as partições no disco Olá não estão em uso. Certifique-se de sistema operacional Olá não tenta tooremount-las após uma reinicialização. Essas etapas Desfazer configuração Olá provavelmente criou quando [anexando](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco hello.

1. Saudação de uso `lsscsi` identificador de disco do comando toodiscover hello. O `lsscsi` pode ser instalado pelo `yum install lsscsi` (distribuições baseadas no Red Hat) ou pelo `apt-get install lsscsi` (distribuições baseadas no Debian). Você pode encontrar o identificador de disco Olá que procurando usando o número LUN de saudação. último número Olá Olá tupla em cada linha é hello LUN. Em Olá seguinte exemplo de `lsscsi`, LUN 0 mapeia muito  */desenvolvimento/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Use `fdisk -l <disk>` toodiscover partições de saudação associadas Olá disco toobe desanexado. Olá, exemplo a seguir mostra a saída de hello para `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Desmonte cada partição listada para disco hello. Olá exemplo a seguir desmonta `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Saudação de uso `blkid` Olá de toodiscovery comando UUIDs para todas as partições. saudação de saída é similar toohello exemplo a seguir:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Remover as entradas nos Olá **/etc/fstab** arquivo associado com caminhos de dispositivo de saudação ou UUIDs para todas as partições de saudação disco toobe desanexado.  As entradas para este exemplo poderiam ser:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    ou o
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Desanexar o disco Olá
Depois de localizar o número LUN de saudação do disco de saudação e referências de sistema operacional Olá removido, você está pronto toodetach-lo:

1. Desanexar o disco selecionado de saudação da máquina virtual de saudação executando o comando Olá `azure vm disk detach
   <virtual-machine-name> <LUN>`. Olá, exemplo a seguir desanexa LUN `0` de saudação VM denominada `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. Você pode verificar se o disco de saudação foi desanexado executando `azure vm disk list` novamente. Olá verificações de exemplo a seguir Olá VM denominada `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    saudação de saída é similar toohello exemplo, que mostra o disco de dados Olá não esteja conectado a seguir:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

disco Olá desanexado permanece no armazenamento, mas não está mais anexado tooa virtual machine.

