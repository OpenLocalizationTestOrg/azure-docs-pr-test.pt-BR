
1. Entrar tooyour assinatura do Azure usando Olá etapas listadas na [conectar tooAzure do hello Azure CLI 1.0](../articles/xplat-cli-connect.md).

2. Verifique se que você está no modo de implantação clássico Olá da seguinte maneira:

    ```azurecli
    azure config mode asm
    ```

3. Descubra imagem do Linux Olá que você deseja tooload de imagens disponíveis Olá da seguinte maneira:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    Em uma janela de prompt de comando do Windows, use **find** em vez de grep.
   
4. Use `azure vm create` toocreate uma VM com a imagem do Linux Olá na lista anterior de saudação. Esta etapa cria uma conta de armazenamento e um serviço de nuvem. Você também pode se conectar a esse serviço de nuvem existente do VM tooan com um `-c` opção. Criar um toolog de ponto de extremidade SSH na máquina de virtual do Linux toohello com hello `-e` opção. Olá, exemplo a seguir cria uma VM denominada `myVM` usando Olá `Ubuntu-14_04_4-LTS` imagem no hello `West US` local e adiciona um nome de usuário `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Para uma máquina virtual Linux, você deve fornecer Olá `-e` opção `vm create`. Não é possível tooenable SSH depois de máquina virtual de saudação foi criada. Para obter mais detalhes sobre SSH, leia [como tooUse SSH com Linux no Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. Você pode verificar os atributos de saudação do hello VM usando Olá `azure vm show` comando. Olá exemplo a seguir lista as informações para Olá VM denominada `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Iniciar a VM com hello `azure vm start` comando da seguinte maneira:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Próximas etapas
Para obter detalhes sobre todos esses comandos de máquina virtual do Azure CLI 1.0, leia Olá [usando Olá 1.0 da CLI do Azure com a API de implantação clássico Olá](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

