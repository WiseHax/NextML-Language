# Migration Guide: HTML/CSS/JS to NexML

## 1. Overview
This guide helps you migrate existing web projects from traditional HTML/CSS/JavaScript to NexML.

---

## 2. Migration Strategy

### 2.1 Incremental Migration
- Start with small components  
- Migrate page by page  
- Use interoperability features  

### 2.2 Hybrid Approach
- Run NexML alongside existing code  
- Gradual replacement of components  
- Shared state management  

---

## 3. HTML to NexML

### 3.1 Basic Elements

**HTML:**
```html
<div class="container" id="main">
    <h1>Welcome</h1>
    <p>This is a paragraph</p>
    <button onclick="handleClick()">Click me</button>
</div>
```

**NexML:**
```nexml
Div @Main {
    Class: "container"
    
    H1 { "Welcome" }
    P { "This is a paragraph" }
    Button {
        "Click me"
        On:Click HandleClick()
    }
}
```

### 3.2 Forms and Inputs

**HTML:**
```html
<form onsubmit="handleSubmit(event)">
    <input type="text" id="username" name="username" required>
    <input type="email" id="email" name="email">
    <button type="submit">Submit</button>
</form>
```

**NexML:**
```nexml
Form @UserForm {
    On:Submit HandleSubmit(@Event)
    
    Input @UsernameInput {
        Type: "text"
        Name: "username"
        Required: true
        Placeholder: "Enter username"
    }
    
    Input @EmailInput {
        Type: "email" 
        Name: "email"
        Placeholder: "Enter email"
    }
    
    Button {
        Type: "submit"
        "Submit"
    }
}
```

---

## 4. CSS to NexML Styles

### 4.1 Basic Styling

**CSS:**
```css
.container {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
    max-width: 1200px;
    margin: 0 auto;
}

.container:hover {
    background: #e9ecef;
    transform: translateY(-2px);
}
```

**NexML:**
```nexml
Div @Container {
    Style {
        Background: "#f8f9fa"
        Padding: "20px"
        BorderRadius: "8px"
        MaxWidth: "1200px"
        Margin: "0 auto"
        
        States {
            Hover {
                Background: "#e9ecef"
                Transform: "translateY(-2px)"
            }
        }
    }
}
```

### 4.2 Media Queries

**CSS:**
```css
@media (max-width: 768px) {
    .container {
        padding: 10px;
        margin: 10px;
    }
}
```

**NexML:**
```nexml
Div @Container {
    Style {
        Padding: "20px"
        Margin: "0 auto"
        
        Media: (MaxWidth: 768px) {
            Padding: "10px"
            Margin: "10px"
        }
    }
}
```

---

## 5. JavaScript to NexML Scripts

### 5.1 Variables and State

**JavaScript:**
```javascript
let counter = 0;
const user = {
    name: 'John',
    email: 'john@example.com'
};
const items = [];
```

**NexML:**
```nexml
Script {
    Data {
        Counter: 0
        User: {
            Name: "John"
            Email: "john@example.com"
        }
        Items: []
    }
}
```

### 5.2 Functions and Event Handlers

**JavaScript:**
```javascript
function incrementCounter() {
    counter++;
    updateDisplay();
}

function addItem(item) {
    items.push(item);
    counter = items.length;
}

document.getElementById('myButton').addEventListener('click', incrementCounter);
```

**NexML:**
```nexml
Script {
    Function IncrementCounter() {
        @Data.Counter += 1
    }
    
    Function AddItem(item) {
        @Data.Items.Push(item)
        @Data.Counter = @Data.Items.Length
    }
}

Button @MyButton {
    "Click me"
    On:Click IncrementCounter()
}
```

### 5.3 DOM Manipulation

**JavaScript:**
```javascript
const element = document.getElementById('myElement');
element.style.color = 'red';
element.textContent = 'Updated text';

element.addEventListener('animationend', () => {
    element.remove();
});
```

**NexML:**
```nexml
Div @MyElement {
    "Updated text"
    Style {
        Color: "red"
    }
    
    On:AnimationEnd {
        @MyElement.Remove()
    }
}
```

---

## 6. Component Migration

### 6.1 React Components

**React:**
```jsx
function UserCard({ user, onSelect }) {
    return (
        <div className="user-card" onClick={() => onSelect(user)}>
            <img src={user.avatar} alt={user.name} />
            <h3>{user.name}</h3>
            <p>{user.email}</p>
        </div>
    );
}
```

**NexML:**
```nexml
Component UserCard @UserCardComponent {
    Props {
        User: Object
        OnSelect: Function
    }
    
    Template {
        Div @CardContainer {
            Class: "user-card"
            On:Click @OnSelect(@User)
            
            Img {
                Source: @User.Avatar
                Alt: @User.Name
            }
            
            H3 { @User.Name }
            P { @User.Email }
        }
    }
}
```

### 6.2 Vue Components

**Vue:**
```vue
<template>
    <div class="counter">
        <button @click="decrement">-</button>
        <span>{{ count }}</span>
        <button @click="increment">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            count: 0
        }
    },
    methods: {
        increment() {
            this.count++
        },
        decrement() {
            this.count--
        }
    }
}
</script>
```

**NexML:**
```nexml
Component Counter @CounterComponent {
    Script {
        Data {
            Count: 0
        }
        
        Function Increment() {
            @Data.Count += 1
        }
        
        Function Decrement() {
            @Data.Count -= 1
        }
    }
    
    Template {
        Div @CounterContainer {
            Class: "counter"
            
            Button {
                "-"
                On:Click Decrement()
            }
            
            Span @CountDisplay { "{@Data.Count}" }
            
            Button {
                "+"
                On:Click Increment()
            }
        }
    }
}
```

---

## 7. Animation Migration

### 7.1 CSS Animations

**CSS:**
```css
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.fade-in {
    animation: fadeIn 0.5s ease-in;
}
```

**NexML:**
```nexml
Animation @FadeIn {
    KeyFrames {
        From {
            Opacity: 0
        }
        To {
            Opacity: 1
        }
    }
    
    Duration: "0.5s"
    Timing: "ease-in"
}

Div @AnimatedElement {
    "Content"
    Animations {
        Entrance: "@FadeIn"
    }
}
```

### 7.2 JavaScript Animations

**JavaScript:**
```javascript
function animateElement(element) {
    element.animate([
        { transform: 'translateX(0px)' },
        { transform: 'translateX(100px)' }
    ], {
        duration: 1000,
        easing: 'ease-in-out'
    });
}
```

**NexML:**
```nexml
Div @AnimatedElement {
    "Content"
    Animations {
        Entrance: "slideRight 1s ease-in-out"
    }
}
```

---

## 8. Best Practices

### 8.1 Migration Order
- Start with static components  
- Migrate styling and layout  
- Add interactivity and state  
- Implement complex animations  
- Optimize performance  

### 8.2 Testing Strategy
- Unit test components individually  
- Integration test component interactions  
- End-to-end test critical user flows  
- Performance test animations  

### 8.3 Performance Considerations
- Use lazy loading for large components  
- Implement virtual scrolling for long lists  
- Optimize animation performance  
- Use efficient state updates  

---

## 9. Common Pitfalls

### 9.1 State Management
- Avoid deeply nested state  
- Use computed properties for derived state  
- Implement proper state cleanup  

### 9.2 Event Handling
- Remember event propagation  
- Use proper event delegation  
- Clean up event listeners  

### 9.3 Animation Performance
- Use transform and opacity for animations  
- Avoid animating layout properties  
- Use will-change for complex animations  
