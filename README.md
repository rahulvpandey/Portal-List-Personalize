#Update :
- Removed Multiselect.js dependencies
- Added reordering of columns
- Fixed multiple removal bug
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
 
**Add below code to your Data Widget's Server Side code** 
```
function CheckPreference(table, view){
	var userPref = new GlideRecord('sys_user_preference');
		userPref.addQuery('name', table+'_'+view+'_list.view');
		userPref.addQuery('user', gs.getUserID());
		userPref.query();
		if (userPref.next()) {
return userPref.value;
		}
}
```

```
data.fields_array = data.fields.split(',');
```
**changes to below**
```
data.fields_array = CheckPreference(data.table, data.view).split(',') || data.fields.split(',');
```

**Add below code to your Data Widget's Server Side code** 

```
var personalizeObj = {};
	personalizeObj.table = data.table;
	personalizeObj.view = data.view;
	data.personalizeParms = personalizeObj;
```
**Import Attached UI script and Widget** 
