# ckz54 VS Code Snippets
Collection of VS Code snippets for Salesforce's B2B Commerce (Cloudcraze) projects. Tested for 4.8 to 4.10.

## Snippets

### Setup

* `gitignore`: My default gitignore for cloudcraze/B2B commerce projects.

E.g. 
```
# ignore VCode config files
force.json
sfdx-project.json
.forceCode
.sfdx
.vscode
*.code-workspace
*.log

# ignore classes, components, pages, static resources and metas from salesforce...
*.cls
*.cls-meta.xml
*.component
*.component-meta.xml
*.page
*.page-meta.xml
*.resource
*.resource-meta.xml
*.trigger
*.trigger-meta.xml

# ...with the exception of the package.xml and anything that starts with the naming convention
!package.xml
!$1_*
!README.MD
```

* `package`: Basic Package.xml for Salesforce B2B Commerce projects. Retrieves the top CC objects and related types (in case you want to add fields programmatically, like I do)

E.g.
```
<?xml version='1.0' encoding='UTF-8'?>
  <Package xmlns='http://soap.sforce.com/2006/04/metadata'>
      <types>
          <members>*</members>
          <name>ApexClass</name>
      </types>
      <types>
          <members>*</members>
          <name>ApexTrigger</name>
      </types>
      <types>
          <members>*</members>
          <name>ApexComponent</name>
      </types>
      <types>
          <members>*</members>
          <name>ApexPage</name>
      </types>
     <types>
         <members>*</members>
         <name>StaticResource</name>
     </types>
 
      <types>
          <members>Admin</members>
          <members>B2B Customer Community Plus User</members>
          <members>B2B Customer Community User</members>
          <name>Profile</name>
      </types>
      <types>
          <members>ccrz__E_Product__c</members>
          <members>ccrz__E_Category__c</members>
          <members>ccrz__E_Attribute__c</members>
          <members>ccrz__E_ProductCategory__c</members>
          <members>ccrz__E_Spec__c</members>
          <members>ccrz__E_ProductSpec__c</members>
          <members>ccrz__E_ProductMedia__c</members>
          <members>ccrz__E_PriceList__c</members>
          <members>ccrz__E_PriceListItem__c</members>
          <members>ccrz__E_Cart__c</members>
          <members>ccrz__E_CartItem__c</members>
          <members>ccrz__E_Order__c</members>
          <members>ccrz__E_OrderItem__c</members>
          <name>CustomObject</name>
      </types>
      <types>
          <members>ccrz__E_Product__c-ccrz__CC Product Layout</members>
          <members>ccrz__E_Category__c-ccrz__CC Category Layout</members>
          <members>ccrz__E_Attribute__c-ccrz__CC Attribute Layout</members>
          <members>ccrz__E_ProductCategory__c-ccrz__CC Product Category Layout</members>
          <members>ccrz__E_Spec__c-ccrz__CC Spec Layout</members>
          <members>ccrz__E_ProductSpec__c-ccrz__CC Product Spec Layout</members>
          <members>ccrz__E_ProductMedia__c-ccrz__CC Product Media Layout</members>
          <members>ccrz__E_PriceList__c-ccrz__CC Price List Layout</members>
          <members>ccrz__E_PriceListItem__c-ccrz__CC Price List Item Layout</members>
          <members>ccrz__E_Cart__c-ccrz__CC Cart Layout</members>
          <members>ccrz__E_CartItem__c-ccrz__CC Cart Item Layout</members>
          <members>ccrz__E_Order__c-ccrz__CC Order Layout</members>
          <members>ccrz__E_OrderItem__c-ccrz__CC Order Item Layout</members>
          <name>Layout</name>
      </types>
 <!--
     <types>
         <members>*</members>
         <name>Flow</name>
     </types>
     <types>
         <members>*</members>
         <name>FlowDefinition</name>
     </types>
     <types>
         <members>*</members>
         <name>Workflow</name>
     </types>
 -->
      <version>45.0</version>
  </Package>
  ```

### Visualforce Pages

* `apex_page`: Default apex header for VF communities. It makes it easier to not forget the 4 declaration headers to prevent Salesforce to add extra HTML in your pages.

```
<apex:page docType="html-5.0"
    sidebar="false" showHeader="false" standardStylesheets="false" 
    applyHtmlTag="false"
    id="$1" controller="$2">
    

</apex:page>
```

* `script_hbt`: Handlebars template declaration.

```
<script id="$1" type="text/template">
    

</script> <!-- end of $1 hb template -->

```

### Apex Classes

* `ckz_hook`, `ckz_logic`, `ckz_service`: Default hook/logic/service extension declaration

```
global with sharing class $1_$2 extends ccrz.cc_$2 {
	
}
```

* `ckz_method`: Default method override declaration

```
global override Map<String, Object> $1(Map<String, Object> inputData) {
	ccrz.ccLog.log(LoggingLevel.DEBUG,'M:I:$1:inputData',inputData);
	Map<String, Object> retData;
	//calls the super of the method
	retData = super.$1(inputData);
	
	ccrz.ccLog.log(LoggingLevel.DEBUG,'M:X:$1:retData',retData);
}
```

### Javascript files

* `hbt_helper`: Handlebars helper registration

```
Handlebars.registerHelper('$1', function(){
    
} // end of $1 hb helper

```

* `ckz_pubsub`: Generic pubsub on method

```
listenerEvent = $1;
CCRZ.pubsub.on(listenerEvent, function(theView) {
    console.log("$1 triggered");
    
});
```

* `ckz_events`: CC View event override

```
theView.events["$1 $2"] = function(){
    
} // end of $1$2 event
theView.delegateEvents();
```

* `ckz_remote`: Generic remote action invoke

```
// call a custom remote action
this.className = '$1';
//this.invoke*( methodName, [arg0], [arg1], ... [argN], [responseFunction], [callOptions])
this.invokeCtx(
    '$2',
    function(response,event){
        if(event.status){
            console.log("$2 remote action called successfully");
            //do something with the response
            
        }else{
            console.log("$2 remote action called, but something went wrong");
        }
    },
    {
        buffer:false, //this call will be executed by itself
        nmsp : false //defines that this is a call to a subscriber class
    }
);
```
