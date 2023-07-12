Idempotencia é muito importante no terraform, para evitar a criacao de recursos em duplicidade

O codigo do Terraform é de forma declarativa, isto é mostrando o que é desejado como resultado final. Caso esse resultado final seja o mesmo que o já existente ele nao fará nada.

## Terraform x Ansible

Terraform é melhor para criar estruturas (novo cluster, criar um recurso na nuvem) enquando o ansible é melhor para gerenciar configurações (liberar ips, redirecionamento de portas para todas as maquinas, etc)

## Estado

O terraform grava um arquivo de estado, para comparar ao executar novamente. Caso esse arquivo nao exista, sera um problema para criar.

É possivel configurar um arquivo online (bucket s3) para o trabalho em conjunto.

## Inicio

O Padrao para criar um recurso é:

```hcl
resource "local_file" "exemplo"{
    filename = "exemplo.txt"
    content = var.conteudo
}
```
Onde

- "local_file" é a juncao de qual provider que estamos utilizando com o nome do tipo.
- "exemplo" é o nome do recurso na execucao

Por padrao o terraform le o arquivo `terraform.tfvars` como padrao de passar de variaveis enquanto 

É possivel ler recursos ja criados com o `data` (datasource)

```hcl
data "local_file" "conteudo-exemplo"{
    filename = "exemplo.txt"
}
```

É possivel exebir por exemplo em outputs

```
output "data-source-result" {
    value = data.local_file.conteudo-exemplo.content_base64
  
}
```

## variaveis

Por padrao o terraform le o arquivo `terraform.tfvars` como padrao de passar de variaveis enquanto `variables.tf` voce define quais as variaveis disponives

## Count

É possivel passar ao criar o resource um `count` em que o terraform criaria na quantidade passada. 

Alem disso sera possivel utilizar index com `count.index`

## Criando cluster k8s utlizando apenas resources

[link](https://github.com/codeedu/fc2-terraform/tree/resources)

## Criando cluster k8s utlizando apenas modulos

[link](https://github.com/codeedu/fc2-terraform/tree/modules)