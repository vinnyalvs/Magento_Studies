# Plugins (interceptors)

Permitem a modificação de métodos públicos de outras classes sem modificar a classe original. Eles são executados antes ou depois do método original, ou substituem completamente o método original (executam em volta)

## Limitações de plugin: 

* Final Methods e Final Classes 
* Métodos privados, protegidos (protected) ou estáticos
* Métodos --countruct
* Virtual Types
* Objetos de classes que ao instanciadas antes do Interception bootstrap
* Classes que implementam a interface NonInterceptableInterface


## Criação de Plugin

Deve ser feita a definição de plugin no arquivo di.xml

Um exemplo de como definir plugins no di.xml pode ser encontrado [aqui](https://github.com/vinnyalvs/Magento_Experiments/blob/main/app/code/Vinnyalvs/PluginExample/etc/di.xml)

## Glossário:

        Método Observado: Método que queremos alterar o comportamento
        Classe original: Classe que contém o Método Observado
        $subject -> variável com classe original que contém o método a ser observado
        MethodName -> nome do método observado
        $proceed -: callback para o método observado


## Tipos de plugin: 

### before:

* Executam antes do método observado.
* Sempre tem o nome segundo o padrão: beforeMethodName
* No geral são usados para modificar parametros que são enviados para o método observado.
* Recebe: $subject + demais parametros originais do método 
* Retorna: Array com os novos valores dos parametros do método observado. Se o método observado não recebia parametros, então deve retornar null ou nada.

Um exemplo pode ser encontrado [aqui](https://github.com/vinnyalvs/Magento_Experiments/blob/main/app/code/Vinnyalvs/PluginExample/Plugin/Api/NormalizeProductNameBeforeSave.php)


### after:

* Executam após o método observado.
* Sempre tem o nome segundo o padrão: afterMethodName
* No geral são usados para modificar a saída do método observado
* Recebe: $subject + $result + demais parametros originais do método 
* Retorna: Novo resultado do método.

Um exemplo pode ser encontrado [aqui](https://github.com/vinnyalvs/Magento_Experiments/blob/main/app/code/Vinnyalvs/PluginExample/Plugin/Api/LogProductNameAfterSave.php)

### around

* Sobrescrevem o comportamento do método observado.
* Sempre tem o nome segundo o padrão: aroundMethodName
* No geral são usados para modificar o comportamento do método como um todo.
* Recebe: $subject + callback $proceed + demais parametros originais do método 
* Retorna: Novo resultado do método.

#### Observações sobre Around

1. Sempre deve ser chamado o método $proceed
1. O uso do Around é desencorajado pela Adobe pois é difícil de depurar e afeta a performance da loja.


Um exemplo pode ser encontrado [aqui](https://github.com/vinnyalvs/Magento_Experiments/blob/main/app/code/Vinnyalvs/PluginExample/Plugin/Api/LogProductNameAroundSave.php