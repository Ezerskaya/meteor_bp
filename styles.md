# Правила разработки интерфейса

## REM 
Рем всегда равен 16px как оптимальный размер шрифта по умолчанию

## Размеры 
Размеры которые влияют на размер контейнера включая 
- font-size
- padding, margin
- top, left, bottom, right
- line-height
- border-radius

должны быть кратны либо .25rem либо 2rem если размер больше 2rem.

При этоv для 
- box-shadow
- transform

можно задавать произвольные размеры, так как они не влияют на контейнер

## [Порядок свойств в стиле](#general-style-props-order)

1. Position
2. Box
3. Flex
4. Typography
5. Background & Foreground
6. Misc

Пример
````LESS
{
  // Position
  position: absolute;
  top: 0;
  left: 0;
  
  // Box
  display: flex;
  width: 0;
  max-width: 80ch;
  height: auto;
  max-height: 100%;
  padding: 1rem;
  margin: 1rem;
  border: 1px solid red;
  
  // Flex
  flex: 1;
  flex-direction: column;
  
  // Typography
  font-family: sans;
  line-height: 2rem;
  
  // Background & Foreground
  background-color: red;
  
  // Misc
  box-shadow: 2px 2px 2px #ccc;
  transform: translateY(10rem);
}
````

## [БЭМ](#bem)

Все стили блока или элемента лежат только в файле этого блока или элемента. Переопределение стилей блока или элемента из другого блока или элемента строго недопустимо. В случае если отображение или поведение блока/элемента завсят от контекста для этого должны применяться исключительно модификаторы.

Пример грубой ошибки
````LESS
.navbar {
  padding-top: 1rem;

  & .container {
    padding: 0 3rem 0 2.5rem;
  }

  & .grid {
    flex-wrap: wrap;
    justify-content: space-between;
  }
}

````

## [React](#react)

### [Правила работы над компонентом](#react-com-dev-rules)
- Компонент нельзя комитить без документации
- Доработкой компонента может заниматься только его автор указаный в @author
- Версия указывается в формате XX.YY.ZZZZ https://semver.org
- Если YY в версии = 0, значит это прототип и использовать его может только автор
- Если нужно увеличть XX - новая версия компонета с потерей совместимости, то новй компонент должен называться ComponentName2 а старая версия помечена как @deprecated, соответственно для разработки версии с потерей совместимости нужно создать отдельный компонент, чтобы старый все еще можно было использовать до официальной миграции, после миграции и удаления старого компонента новый может быть избавлен от версии в названии
- Если автор недоступен, то должен быть добавлен или соавтор или изменен основной автор
- Если версия модуля, компонента или подкомпонентов 

Пример документации компонента 
````JavaScript
/** ComponentName to use like this and this
 *  @module ComponentName
 *  @author username
 *  @version 0.0.1
 */
 
 import React from 'react'
 
 ...
````

### [Структура компонента](#react-com-structure)

Общее
- Компонент может содержать и экспортировать подкомпоненты
- Каждый компонент сразу должен быть задокументирован в JSDoc без комментариев нельзя комитить компоненты
- Для создания компонентов нужно использовать только полные функции а не классы или стрелочные функции
- Имя функции компонента, как требует Реакт дается в PascalCse
- Имена файлов и css-классов в компоненте в camelCase
- Подкомпонент отделяется от компонента _ и называются в camelCase

Структура файлов в компоненте
````Shell
/componentName
  index.js
  componentName.js
  componentName.less
  somponentName_sub1.js
  somponentName_sub2.less
  somponentName_sub2.js
  somponentName_sub2.less
````

index.js
````JavaScript
export * from './componentName.js'
export * from './somponentName_sub1.js'
export * from './somponentName_sub2.js'
````

componentName.js
````JavaScript
/** ComponentName to use like this and this
 *
 *  @author username
 *  @version 0.0.1
 */
 
import React from 'react'

/** Component description
 *  @param props
 *  @param props.children
 *  @return {any}
 */
export function ComponentName(props) {
  return (
    <div className="componentName">{props.children}</div>
  )
}
````

componentName_sub1.js
````JavaScript
import React from 'react'

/** Sub Component description
 *  @param props
 *  @param props.children
 *  @return {any}
 */
export function ComponentName_sub1(props) {
  return (
    <div className="componentName_sub1">{props.children}</div>
  )
}
````
