# NexML Language Specification

## 1. Introduction
**NexML (Next Markup Language)** is a unified web development language that combines **HTML structure**, **CSS styling**, and **JavaScript logic** into a single, cohesive syntax.

---

## 2. Language Overview

### 2.1 Design Principles
- **Unified Syntax**: Single language for structure, style, and logic  
- **Reactive by Default**: Built-in state management and reactivity  
- **Component-Based**: Modular and reusable components  
- **Animation First**: Native animation system  
- **Type Safe**: Optional type system for better tooling  

### 2.2 Core Concepts
- **Elements**: Basic building blocks (equivalent to HTML elements)  
- **Components**: Reusable, parameterized elements  
- **Styles**: Inline styling with CSS-like syntax  
- **Scripts**: Embedded logic and state management  
- **Animations**: Built-in animation system  

---

## 3. Syntax Grammar

### 3.1 Basic Structure
```ebnf
App ::= Identifier '{' Head? Body '}'
Head ::= 'Head' '{' HeadContent* '}'
Body ::= 'Body' '{' BodyContent* '}'
```

### 3.2 Element Declaration
```ebnf
Element ::= Identifier ('@' Identifier)? '{' ElementContent* '}'
ElementContent ::= Text | Attribute | Style | Script | Animation
```

### 3.3 Component Declaration
```ebnf
Component ::= 'Component' Identifier '@' Identifier '{' Props? Template '}'
Props ::= 'Props' '{' PropDeclaration* '}'
PropDeclaration ::= Identifier ':' Type ('=' DefaultValue)?
```

---

## 4. Type System

### 4.1 Basic Types
- `String`: Text values  
- `Number`: Numeric values  
- `Boolean`: True/False values  
- `Array`: Collections of values  
- `Object`: Key-value pairs  
- `Function`: Callable procedures  

### 4.2 Advanced Types
- `Component`: Reusable UI elements  
- `Animation`: Animation definitions  
- `Event`: User interaction handlers  

---

## 5. Execution Model

### 5.1 Compilation Phase
1. **Lexical Analysis**: Tokenize source code  
2. **Parsing**: Build Abstract Syntax Tree (AST)  
3. **Transformation**: Optimize and validate AST  
4. **Code Generation**: Output HTML, CSS, JavaScript  

### 5.2 Runtime Phase
1. **Initialization**: Load components and state  
2. **Rendering**: Generate DOM elements  
3. **Binding**: Connect events and reactivity  
4. **Animation**: Process animation timelines  

---

## 6. Security Model

### 6.1 Sandboxing
- Component isolation  
- Secure event handling  
- XSS prevention  

### 6.2 Data Validation
- Type checking at compile time  
- Runtime validation  
- Input sanitization  

---

## 7. Compliance Levels

### 7.1 Level 1 (Basic)
- Element rendering  
- Basic styling  
- Event handling  

### 7.2 Level 2 (Standard)
- Component system  
- State management  
- Basic animations  

### 7.3 Level 3 (Advanced)
- Advanced animations  
- Type system  
- Performance optimizations  
