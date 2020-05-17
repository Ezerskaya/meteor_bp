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

## Порядок свойств в стиле 

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
  line-height: 2rem
  
  // Colors
  background: red;
  
  // Misc
  box-shadow: 2px 2px 2px #ccc;
  transform: translateY(10rem);
}
```

