# ACL (Access Control List)

Para um usuário administrador, é possível atribuir alguns papéis (roles) especificas que permitem regular (permitindo ou negando) o acesso desse usuário a recursos e funcionalidades da plataforma. Esses recursos podem ser acesso a menus do admin, endpoints de API, controllers e até renderizar ou não alguns blocos de layout. 

Um aquivo ACL permite definir recursos customizados e depois podemos definir quais roles tem acesso a esses recursos. 

Adobe Documentation: https://developer.adobe.com/commerce/php/tutorials/backend/create-access-control-list-rule/

## Exemplo de arquivo acl.xml

Um exemplo de arquivo acl pode ser visto na documentação oficial e um exemplo prático [aqui](https://github.com/vinnyalvs/Magento_Experiments/blob/main/app/code/Vinnyalvs/AdminController/etc/acl.xml)
.

No arquivo xml, dentro da tag <config> nós temos a tag <acl> e a tag <resources> e por fim uma tag <resource>. Cada resource pode ter um resource no interior. 

        <?xml version="1.0"?>
        <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Acl/etc/acl.xsd">
        <acl>
        <resources>
                <resource id="Magento_Backend::admin">
                <resource id="Vendor_MyModule::menu" title="Custom Menu" sortOrder="10" >
                <resource id="Vendor_MyModule::create" title="Create" sortOrder="50" />
                </resource>
                </resource>
        </resources>
        </acl>
        </config>

Atributos do arquivo etc/acl.xml

| Campo       | Descrição                                                                 |
|-------------|----------------------------------------------------------------------------|
| id          | String única. Deve estar no formato `Vendor_ModuleName::resourceName`       |
| title       | Título exibido na barra de menu                                             |
| sortOrder   | Posição em que o menu é exibido 



Lembrando que a prioridade na sortOrder é crescente, ou seja um item com valor sortOrder 10 será exibido antes de um com sortOrder 50.

## Restringindo acesso

Para controlar o acesso no item que nós queremos restringir devemos associar a ele o resource desejado. Isso pode ser feito em arquivos menu.xml, arquivos webapi.xml e arquivos de layout. Nos arquivos menu.xml e webapi.xml nos referimos como resource e nos de layout como aclResource.

Exemplo

### menu.xml

        <?xml version="1.0"?>
                <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Backend:etc/menu.xsd">
                        <menu>
                                <add id="Vendor_MyModule::menu" title="Custom Menu" module="Vendor_MyModule" sortOrder="10" resource="Vendor_MyModule::menu"/>
                         </menu>
                </config>
        </xml>


### Arquivos de Layout

        <block class="Vendor\MyModule\Block\Adminhtml\Type" name="block.example" aclResource="Vendor_MyModule::view_additional">
        <!-- ... -->
        </block>

### webapi.xml

        <?xml version = "1.0"?>
        <routes xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Webapi:etc/webapi.xsd">
        <route url="/V1/admin/create" method="POST">
                <service class="Vendor\MyModule\Api\Create" method="execute"/>
                <resources>
                <resource ref="Vendor_MyModule::create" />
                </resources>
        </route>
        </routes>

Outro exemplo [aqui](https://github.com/vinnyalvs/Magento_Experiments/blob/main/app/code/Vinnyalvs/AdminController/etc/acl.xml)

### Também é possível restringir admin controllers

Basta usar a constante ADMIN_RESOURCE no controller de ação ou página.

        const ADMIN_RESOURCE = 'Vendor_MyModule::create'

Tem um exemplo [aqui](https://github.com/vinnyalvs/Magento_Experiments/blob/main/app/code/Vinnyalvs/AdminController/\Controller\Adminhtml\Pets\Show.php)
