# CreateSpaces2021
Адаптация макроса CreateSpaces для Revit из шаблонов ADSK 2019 для версии 2021.

В чатах по шаблонам ADSK часто задают вопрос, как можно адаптировать макрос создания пространств, который содержится в шаблонах ADSK 2019 в более свежие версии. Для своих нужд я уже адаптировал его в виде плагина для версии 2021 (да, я знаю, что он есть в плагине BIM2B, но вот была такая производственная необходимость, чтоб отдельно был 😀). И я решил написать эту небольшую инструкцию о том как это сделать так, как я сам это понимаю.

В Initial commit находится исходная версия, просто скопированная из проекта на шаблоне 2019 в проект на шаблоне 2021.
Далее - что нужно изменит.
Директивы, которые нужно добавить (имеется в виду, к стандартному шаблону макроса, который идёт по умолчанию с Revit 2021):
using Autodesk.Revit.DB.Architecture;
using Autodesk.Revit.DB.Mechanical;
using System.Diagnostics;

Заменить:
```
this.Application.ActiveUIDocument.Selection
```
на
```
this.ActiveUIDocument.Selection
```
в 4 местах.

В строках
```
sp.get_Parameter(BuiltInParameter.ROOM_UPPER_OFFSET).Set(UnitUtils.ConvertToInternalUnits(defLimitOffset, DisplayUnitType.DUT_MILLIMETERS));
wSpace.get_Parameter(BuiltInParameter.ROOM_UPPER_OFFSET).Set(UnitUtils.ConvertToInternalUnits(defLimitOffset, DisplayUnitType.DUT_MILLIMETERS));
```
заменить
```
DisplayUnitType.DUT_MILLIMETERS
```
на
```
UnitTypeId.Millimeters
```

После этого можно компилировать, должно работать.