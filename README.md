# Portal-List-Personalize
Widget to add personalize feature(gear icon) on servicenow Portal list view
![alt text](https://preview.ibb.co/chpcPf/personalize.png)
# Installation
**Add below html code to your Data Widget's html**
```
 <span class="glyphicon glyphicon-cog" ng-click="c.personalize('personalize_list')" aria-hidden="true"></span>
 ```
**Add below services to your Data Widget's client controller**

$rootScope, spModal, $window

**Add below code to your Data Widget's client controller**
```
	$rootScope.$on('personalizationDone', function(event,data) {
		$window.location.reload(); // refresh to new layout
		});
 c.personalize = function(widgetId, widgetInput) {
        spModal.open({
            title: 'Personalize List Columns',
            widget: widgetId, 
            widgetInput: $scope.data.personalizeParms || {}
        }).then(function(){
					$rootScope.$emit('saveChosen');
       
        })      
    }
    ```
    
