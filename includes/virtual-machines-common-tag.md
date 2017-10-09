


## <a name="tagging-a-virtual-machine-through-templates"></a>Marcando uma máquina virtual por meio de modelos
Primeiramente, vamos observar uma marcação por meio de modelos. [Este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) insere marcas no hello recursos a seguir: (Máquina Virtual) de computação, armazenamento (conta de armazenamento) e rede (endereço IP público, rede Virtual e Interface de rede). Esse modelo destina-se a uma VM do Windows, mas pode ser adaptada para VMs do Linux.

Clique em Olá **implantar tooAzure** botão da saudação [link modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Isso vai navegar toohello [portal do Azure](https://portal.azure.com/) onde você pode implantar este modelo.

![Implantação simples com marcas](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Esse modelo inclui Olá marcas a seguir: *departamento*, *aplicativo*, e *criado por*. Você pode adicionar/editar essas marcas diretamente no modelo de saudação se você gostaria que os nomes de marca diferente.

![Marcas do Azure em um modelo](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Como você pode ver, marcas de saudação são definidas como pares chave/valor, separados por dois-pontos (:). marcas de saudação devem ser definidas neste formato:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Salve o arquivo de modelo de saudação depois de terminar de editá-lo com marcas de saudação de sua escolha.

Em seguida, no hello **Editar parâmetros** seção, você pode preencher os valores hello suas marcas.

![Editar marcas no Portal do Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Clique em **criar** toodeploy este modelo com seus valores de marca.

## <a name="tagging-through-hello-portal"></a>Marcação de saudação Portal
Depois de criar os recursos com marcas, você pode exibir, adicionar e excluir marcas no portal de saudação.

Selecione Olá marcas ícone tooview suas marcas:

![Ícone de marcas no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Adicionar uma nova marca por meio do portal Olá definindo seu próprio par chave/valor e salve-o.

![Adicionar nova marca no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

A nova marca agora deve aparecer na lista de saudação de marcas de recurso.

![Nova marca salva no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

