# NexML Syntax Guide

## 1. Basic Syntax

### 1.1 Application Structure
```nexml
App {
    Head {
        Title "My Application"
        Meta Charset="utf-8"
    }
    
    Body {
        // Application content here
    }
}
```

### 1.2 Elements and Attributes
```nexml
// Basic element
Div {
    "Hello World"
    Class: "container"
    Id: "main-content"
}

// Element with reference
Button @SubmitButton {
    "Click Me"
    On:Click HandleSubmit()
}
```

## 2. Styling System

### 2.1 Inline Styles
```nexml
Div @StyledBox {
    "Styled Content"
    Style {
        Background: "#f0f0f0"
        Padding: "20px"
        BorderRadius: "8px"
        FontSize: "16px"
        
        // Responsive design
        Media: (MaxWidth: 768px) {
            Padding: "10px"
            FontSize: "14px"
        }
    }
}
```

### 2.2 Style States
```nexml
Button @InteractiveButton {
    "Hover Me"
    Style {
        Background: "#007bff"
        Color: "white"
        Transition: "all 0.3s ease"
        
        States {
            Hover {
                Background: "#0056b3"
                Transform: "scale(1.05)"
            }
            
            Active {
                Background: "#004085"
                Transform: "scale(0.95)"
            }
            
            Disabled {
                Background: "#6c757d"
                Opacity: 0.6
                Cursor: "not-allowed"
            }
        }
    }
}
```

## 3. Scripting and Logic

### 3.1 Data Declaration
```nexml
Script {
    Data {
        Counter: 0
        User: {
            Name: "John Doe"
            Email: "john@example.com"
            IsActive: true
        }
        Items: ["Apple", "Banana", "Orange"]
    }
    
    // Computed properties
    Computed {
        UserInitials: @User.Name.Split(' ').Map(word => word[0]).Join('')
        ItemCount: @Items.Length
    }
}
```

### 3.2 Functions and Methods
```nexml
Script {
    Function AddItem(newItem) {
        @Data.Items.Push(newItem)
        @Data.Counter = @Data.Items.Length
    }
    
    Function RemoveItem(index) {
        @Data.Items.Splice(index, 1)
        @Data.Counter = @Data.Items.Length
    }
    
    Function ResetAll() {
        @Data.Items = []
        @Data.Counter = 0
    }
}
```

## 4. Event Handling

### 4.1 DOM Events
```nexml
Button @EventButton {
    "Interactive Button"
    
    On:Click {
        @Data.Counter += 1
        Console.Log("Button clicked!")
    }
    
    On:MouseEnter {
        @EventButton.Style.Background = "#28a745"
    }
    
    On:MouseLeave {
        @EventButton.Style.Background = "#007bff"
    }
    
    On:KeyPress(Key: "Enter") {
        SubmitForm()
    }
}
```

### 4.2 Custom Events
```nexml
Component CustomModal @MyModal {
    Props {
        IsOpen: Boolean = false
        OnClose: Function
    }
    
    Template {
        Div @ModalOverlay {
            Style {
                Display: @IsOpen ? "flex" : "none"
                // ... modal styles
            }
            
            On:Click @OnClose
        }
    }
}
```

## 5. Conditional Rendering

### 5.1 If/Else Statements
```nexml
Div @ConditionalContent {
    If: @User.IsLoggedIn {
        WelcomeMessage @Welcome {
            UserName: @User.Name
        }
        
        Button {
            "Logout"
            On:Click Logout()
        }
    }
    
    Else: {
        LoginForm @AuthForm {
            On:Success {
                @User.IsLoggedIn = true
                @User.Name = @AuthForm.UserName
            }
        }
    }
}
```

### 5.2 Switch Statements
```nexml
Div @StatusDisplay {
    Switch: @Data.Status {
        Case: "loading" {
            LoadingSpinner {}
        }
        
        Case: "success" {
            SuccessMessage {
                "Operation completed successfully!"
            }
        }
        
        Case: "error" {
            ErrorMessage {
                "An error occurred: {@Data.ErrorMessage}"
            }
        }
        
        Default: {
            Text "Ready"
        }
    }
}
```

## 6. Loops and Lists

### 6.1 Basic Loops
```nexml
Ul @ItemList {
    For Each: @Data.Items As: item Index: index {
        Li @{`item-${index}`} {
            "{item}"
            
            Style {
                AnimationDelay: "${index * 0.1}s"
            }
            
            On:Click {
                RemoveItem(index)
            }
        }
    }
}
```

### 6.2 Object Iteration
```nexml
Div @UserProfile {
    For Each: @User As: value Key: key {
        Div @{`profile-${key}`} {
            Strong "{key.Capitalize()}: "
            Span "{value}"
        }
    }
}
```

## 7. Component System

### 7.1 Component Definition
```nexml
Component UserCard @UserCardComponent {
    Props {
        User: Object
        ShowAvatar: Boolean = true
        OnSelect: Function?
    }
    
    Template {
        Div @CardContainer {
            Style {
                Border: "1px solid #ddd"
                BorderRadius: "12px"
                Padding: "16px"
                Cursor: @OnSelect ? "pointer" : "default"
            }
            
            On:Click @OnSelect?.(@User)
            
            If: @ShowAvatar {
                Img {
                    Source: @User.Avatar ?? "/default-avatar.png"
                    Alt: "{@User.Name}'s avatar"
                }
            }
            
            Heading @UserName { @User.Name }
            Text @UserEmail { @User.Email }
        }
    }
}
```

### 7.2 Component Usage
```nexml
Div @UserGrid {
    For Each: @Data.Users As: user {
        UserCard {
            User: user
            ShowAvatar: true
            OnSelect: HandleUserSelect
        }
    }
}
```

## 8. Animation System

### 8.1 Built-in Animations
```nexml
Div @AnimatedElement {
    "Animated Content"
    Style {
        Opacity: 0
        Transform: "translateY(20px)"
    }
    
    Animations {
        Entrance: "fadeInUp 0.6s ease-out"
        Exit: "fadeOutDown 0.4s ease-in"
        Hover: "pulse 0.5s"
    }
}
```

### 8.2 Custom Animations
```nexml
Animation @BounceEffect {
    KeyFrames {
        "0%, 20%, 53%, 80%, 100%" {
            Transform: "translate3d(0,0,0)"
        }
        "40%, 43%" {
            Transform: "translate3d(0,-30px,0)"
        }
        "70%" {
            Transform: "translate3d(0,-15px,0)"
        }
        "90%" {
            Transform: "translate3d(0,-4px,0)"
        }
    }
    
    Duration: "1s"
    Timing: "ease-in-out"
    Iteration: "infinite"
}
```

## 9. Advanced Features

### 9.1 Reactive Programming
```nexml
Script {
    Watch: @Data.Counter {
        If: @Data.Counter > 10 {
            ShowNotification("Counter reached 10!")
        }
    }
    
    Watch: @User.Name {
        Immediate: true
        Handler(newName, oldName) {
            Console.Log(`User name changed from ${oldName} to ${newName}`)
        }
    }
}
```

### 9.2 Lifecycle Hooks
```nexml
Component SmartComponent @SmartComponent {
    On:Mount {
        Console.Log("Component mounted")
        FetchData()
    }
    
    On:Update {
        Console.Log("Component updated")
    }
    
    On:Unmount {
        Console.Log("Component unmounted")
        Cleanup()
    }
    
    Template {
        // Component content
    }
}
```
