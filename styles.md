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

При это для 
- box-shadow
- transform

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
  height: auto;
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

## React

### Структура компонента

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
import React from 'react'

/**
 * Component description
 * @param props
 * @param props.children
 * @return {any}
export function ComponentName(props) {
  return (
    <div className="componentName">{props.children}</div>
  )
}
````

componentName_sub1.js
````JavaScript
import React from 'react'

/**
 * Sub Component description
 * @param props
 * @param props.children
 * @return {any}
export function ComponentName_sub1(props) {
  return (
    <div className="componentName_sub1">{props.children}</div>
  )
}
````
