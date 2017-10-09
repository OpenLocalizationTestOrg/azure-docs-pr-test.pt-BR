
Para saber mais sobre discos, consulte [Sobre discos e VHDs para máquinas virtuais](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Anexar um disco vazio
1. Abra o Azure CLI 1.0 e [conectar tooyour assinatura do Azure](../articles/xplat-cli-connect.md). Verifique se você está no modo de Gerenciamento de Serviços do Azure (`azure config mode asm`).
2. Digite `azure vm disk attach-new` toocreate e anexar um novo disco, conforme mostrado no exemplo a seguir de saudação. Substituir *myVM* com o nome da saudação de sua máquina Virtual do Linux e especifique o tamanho de saudação do disco de saudação em GB, que é *100GB* neste exemplo:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Depois que o disco de dados Olá é criado e anexado, ele é listado na saída de saudação do `azure vm disk list <virtual-machine-name>` conforme mostrado no exemplo a seguir de saudação:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Anexar um disco existente
Anexar um disco existente exige que você tenha um .vhd disponível em uma conta de armazenamento.

1. Abra o Azure CLI 1.0 e [conectar tooyour assinatura do Azure](../articles/xplat-cli-connect.md). Verifique se você está no modo de Gerenciamento de Serviços do Azure (`azure config mode asm`).
2. Verifique se o hello VHD que você deseja tooattach já está carregado tooyour assinatura do Azure:
   
    ```azurecli
    azure vm disk list
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Se você não encontrar o disco de saudação que você deseja toouse, você pode carregar uma assinatura de tooyour local do VHD usando `azure vm disk create` ou `azure vm disk upload`. Um exemplo de `disk create` seria como Olá exemplo a seguir:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   Você também pode usar `azure vm disk upload` tooupload uma conta de armazenamento específica de tooa do VHD. Leia mais sobre Olá comandos toomanage os discos de dados de máquina virtual do Azure [aqui](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Agora você anexar Olá desejado VHD tooyour VM:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Certifique-se de que tooreplace *myVM* com o nome da saudação de sua máquina virtual, e *myVHD* com seu VHD desejado.

5. Você pode verificar disco Olá é máquina virtual anexado toohello `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Depois de adicionar um disco de dados, você precisa toolog na máquina virtual de toohello e inicializar disco Olá para máquina virtual de saudação pode usar o disco Olá para armazenamento (consulte Olá seguindo as etapas para obter mais informações sobre como toodo inicializar disco Olá).
> 
> 

