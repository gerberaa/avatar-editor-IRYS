# 🚀 IRYS Avatar Creator - Usage Guide

## Table of Contents

1. [Getting Started](#getting-started)
2. [Basic Operations](#basic-operations)
3. [Advanced Techniques](#advanced-techniques)
4. [Workflow Examples](#workflow-examples)
5. [Tips & Tricks](#tips--tricks)
6. [Troubleshooting](#troubleshooting)
7. [Best Practices](#best-practices)

---

## Getting Started

### Quick Start

1. **Open the Application**
   - Open `index.html` in your web browser
   - The application loads automatically with animated background

2. **First Look**
   - **Center**: Avatar canvas (500x500px editing area)
   - **Top**: Upload and Download buttons
   - **Below**: Category tabs (Emojis, Accessories, Custom)
   - **Bottom-left**: Sparait mascot (click for help)
   - **Right**: Control panel (appears when element selected)

3. **Create Your First Avatar**
   ```
   Step 1: Click "Upload Avatar" to add a base image (optional)
   Step 2: Click any emoji from the grid to add it to canvas
   Step 3: Click the emoji on canvas to select and edit it
   Step 4: Use sliders to adjust size, rotation, opacity
   Step 5: Click "Download" to save your avatar
   ```

### Interface Overview

```
┌─────────────────────────────────────────────────────────┐
│  IRYS AVATAR EDITOR                    [3D Cube] [Social]│
│                                                         │
│         [Upload Avatar]  [Download]                     │
│                                                         │
│     [😀 Emojis] [👑 Accessories] [🎨 Custom]           │
│                                                         │
│  ┌─────────────────────────────────┐                   │
│  │                                 │    ┌─────────────┐ │
│  │         Avatar Canvas           │    │   Control   │ │
│  │        (500x500px)              │    │    Panel    │ │
│  │                                 │    │             │ │
│  │    [Draggable Elements]         │    │  Sliders &  │ │
│  │                                 │    │  Controls   │ │
│  └─────────────────────────────────┘    └─────────────┘ │
│                                                         │
│  [?] Sparait                        [Floating Particles]│
└─────────────────────────────────────────────────────────┘
```

---

## Basic Operations

### 1. Adding Elements

#### Adding Emojis
```javascript
// Method 1: Click from UI
// 1. Ensure "😀 Emojis" tab is active
// 2. Click any emoji from the 8-column grid
// 3. Emoji appears at position (100px, 100px)

// Method 2: Programmatic
addIcon('😀');  // Adds smiley face
addIcon('❤️');  // Adds heart
addIcon('🎉');  // Adds party emoji
```

#### Adding Accessories
```javascript
// Method 1: Click from UI
// 1. Click "👑 Accessories" tab
// 2. Click any accessory from the 6-column grid
// 3. Accessory appears on canvas

// Method 2: Programmatic
addIcon('👑');  // Adds crown
addIcon('🕶️');  // Adds sunglasses
addIcon('💎');  // Adds diamond
```

#### Adding Custom Images
```javascript
// Method 1: Upload via UI
// 1. Click "🎨 Custom" tab
// 2. Click "📁 Upload Custom Item"
// 3. Select image file (JPG, PNG, GIF, WebP)
// 4. Image appears in personal grid
// 5. Click image to add to canvas

// Method 2: Programmatic
uploadPersonalItem();  // Opens file dialog
// Or directly add if you have data URL:
addPersonalToCanvas('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...');
```

### 2. Selecting Elements

#### Visual Selection
```
1. Click any element on the canvas
2. Element shows cyan border and glowing shadow
3. Control handles appear (cyan rotate, orange resize)
4. Control panel slides in from right side
```

#### Programmatic Selection
```javascript
// Select specific element
const element = document.getElementById('element-123');
selectElement(element);

// Select first draggable element
const firstElement = document.querySelector('.draggable');
selectElement(firstElement);

// Deselect all elements
document.querySelectorAll('.draggable').forEach(el => {
    el.classList.remove('selected');
});
selectedElement = null;
```

### 3. Moving Elements

#### Drag and Drop
```
1. Click and hold any element (not on handles)
2. Drag to desired position
3. Release to place
4. Element follows mouse cursor smoothly
```

#### Programmatic Movement
```javascript
// Move element to specific position
const element = document.getElementById('element-123');
element.style.left = '200px';
element.style.top = '150px';

// Move selected element
if (selectedElement) {
    selectedElement.style.left = '300px';
    selectedElement.style.top = '250px';
}
```

### 4. Resizing Elements

#### Manual Resize
```
1. Select element (click on it)
2. Drag orange resize handle (bottom-right)
3. Element scales proportionally
4. Font size adjusts for emoji elements
```

#### Slider Control
```
1. Select element
2. Use "Size" slider in control panel
3. Range: 1-500 pixels
4. Real-time preview
```

#### Programmatic Resize
```javascript
// Using slider function
updateSelectedSize(120);  // Sets to 120px

// Direct CSS manipulation
const element = document.getElementById('element-123');
element.style.width = '80px';
element.style.height = '80px';
if (element.textContent) {
    element.style.fontSize = '80px';  // For emoji elements
}
```

### 5. Rotating Elements

#### Manual Rotation
```
1. Select element (click on it)
2. Drag cyan rotate handle (top-right)
3. Element rotates around its center
4. Angle updates in real-time
```

#### Slider Control
```
1. Select element
2. Use "Rotation" slider in control panel
3. Range: 0-360 degrees
4. Smooth rotation animation
```

#### Programmatic Rotation
```javascript
// Using slider function
updateSelectedRotation(45);  // Rotates 45 degrees

// Direct CSS manipulation
const element = document.getElementById('element-123');
element.style.transform = 'rotate(45deg)';

// Preserve other transforms
const currentTransform = element.style.transform || '';
const withoutRotate = currentTransform.replace(/rotate\([^)]*\)/g, '').trim();
const newTransform = withoutRotate ? 
    `${withoutRotate} rotate(45deg)` : 
    'rotate(45deg)';
element.style.transform = newTransform;
```

### 6. Adjusting Opacity

#### Slider Control
```
1. Select element
2. Use "Opacity" slider in control panel
3. Range: 0-100%
4. 0% = completely transparent
5. 100% = completely opaque
```

#### Programmatic Opacity
```javascript
// Using slider function
updateSelectedOpacity(75);  // Sets to 75% opacity

// Direct CSS manipulation
const element = document.getElementById('element-123');
element.style.opacity = '0.75';  // 75% opacity
```

### 7. Managing Layers (Z-Index)

#### Slider Control
```
1. Select element
2. Use "Layer" slider in control panel
3. Range: 1-100
4. Higher numbers = in front
5. Lower numbers = behind
```

#### Programmatic Layering
```javascript
// Using slider function
updateSelectedZIndex(50);  // Sets layer to 50

// Direct CSS manipulation
const element = document.getElementById('element-123');
element.style.zIndex = '50';

// Bring to front
element.style.zIndex = '100';

// Send to back
element.style.zIndex = '1';
```

### 8. Deleting Elements

#### UI Deletion
```
1. Select element (click on it)
2. Click "Delete Element" button in control panel
3. Element is removed immediately
4. Control panel hides automatically
```

#### Programmatic Deletion
```javascript
// Delete selected element
deleteSelected();

// Delete specific element
const element = document.getElementById('element-123');
element.remove();

// Delete all elements
document.querySelectorAll('.draggable').forEach(el => el.remove());
```

---

## Advanced Techniques

### 1. Batch Operations

#### Select and Modify Multiple Elements
```javascript
// Apply same rotation to all elements
const elements = document.querySelectorAll('.draggable');
elements.forEach((element, index) => {
    selectElement(element);
    updateSelectedRotation(index * 30); // 0°, 30°, 60°, etc.
});

// Make all elements semi-transparent
elements.forEach(element => {
    element.style.opacity = '0.7';
});

// Arrange elements in a circle
const centerX = 250, centerY = 250, radius = 100;
elements.forEach((element, index) => {
    const angle = (index * 360 / elements.length) * Math.PI / 180;
    const x = centerX + radius * Math.cos(angle);
    const y = centerY + radius * Math.sin(angle);
    element.style.left = x + 'px';
    element.style.top = y + 'px';
});
```

#### Bulk Element Creation
```javascript
// Create emoji pattern
const emojiPattern = ['😀', '😎', '🎉', '❤️', '⭐'];
emojiPattern.forEach((emoji, index) => {
    addIcon(emoji);
    // Position in a row
    setTimeout(() => {
        const element = document.querySelector('.draggable:last-child');
        element.style.left = (50 + index * 80) + 'px';
        element.style.top = '100px';
    }, 100);
});
```

### 2. Animation Effects

#### Smooth Transitions
```javascript
// Add smooth movement animation
function animateElement(element, targetX, targetY, duration = 1000) {
    element.style.transition = `all ${duration}ms ease-in-out`;
    element.style.left = targetX + 'px';
    element.style.top = targetY + 'px';
    
    // Remove transition after animation
    setTimeout(() => {
        element.style.transition = '';
    }, duration);
}

// Usage
const element = document.querySelector('.draggable');
animateElement(element, 300, 200, 1500);
```

#### Pulsing Effect
```javascript
// Add pulsing animation to element
function addPulseEffect(element) {
    element.style.animation = 'pulse 2s infinite';
}

// CSS for pulse effect (add to stylesheet)
const pulseCSS = `
@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.1); }
}
`;
```

### 3. Custom Element Creation

#### Advanced Element Factory
```javascript
function createAdvancedElement(options) {
    const {
        content,
        x = 100,
        y = 100,
        size = 60,
        rotation = 0,
        opacity = 1,
        zIndex = 10,
        isImage = false
    } = options;
    
    const canvas = document.getElementById('avatarCanvas');
    const element = document.createElement('div');
    
    // Basic setup
    element.className = 'draggable';
    element.style.position = 'absolute';
    element.style.left = x + 'px';
    element.style.top = y + 'px';
    element.style.width = size + 'px';
    element.style.height = size + 'px';
    element.style.transform = `rotate(${rotation}deg)`;
    element.style.opacity = opacity;
    element.style.zIndex = zIndex;
    element.id = 'element-' + Date.now();
    
    // Content setup
    if (isImage) {
        element.style.backgroundImage = `url(${content})`;
        element.style.backgroundSize = 'contain';
        element.style.backgroundRepeat = 'no-repeat';
        element.style.backgroundPosition = 'center';
    } else {
        element.textContent = content;
        element.style.fontSize = size + 'px';
        element.style.display = 'flex';
        element.style.alignItems = 'center';
        element.style.justifyContent = 'center';
    }
    
    // Add control handles
    const rotateHandle = document.createElement('div');
    rotateHandle.className = 'rotate-handle';
    element.appendChild(rotateHandle);
    
    const resizeHandle = document.createElement('div');
    resizeHandle.className = 'resize-handle';
    element.appendChild(resizeHandle);
    
    // Setup interactions
    setupElementInteractions(element);
    canvas.appendChild(element);
    
    return element;
}

// Usage examples
createAdvancedElement({
    content: '🚀',
    x: 200,
    y: 150,
    size: 80,
    rotation: 45,
    opacity: 0.8
});

createAdvancedElement({
    content: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...',
    x: 300,
    y: 200,
    size: 100,
    isImage: true
});
```

### 4. State Management

#### Save Avatar State
```javascript
function saveAvatarState() {
    const elements = Array.from(document.querySelectorAll('.draggable'));
    const state = {
        timestamp: Date.now(),
        elements: elements.map(el => ({
            id: el.id,
            content: el.textContent || el.style.backgroundImage,
            isImage: !!el.style.backgroundImage,
            position: {
                x: parseInt(el.style.left),
                y: parseInt(el.style.top)
            },
            size: {
                width: parseInt(el.style.width),
                height: parseInt(el.style.height)
            },
            transform: el.style.transform,
            opacity: parseFloat(el.style.opacity) || 1,
            zIndex: parseInt(el.style.zIndex) || 10
        }))
    };
    
    // Save to localStorage
    localStorage.setItem('avatarState', JSON.stringify(state));
    return state;
}
```

#### Load Avatar State
```javascript
function loadAvatarState() {
    const savedState = localStorage.getItem('avatarState');
    if (!savedState) return false;
    
    const state = JSON.parse(savedState);
    
    // Clear current canvas
    document.getElementById('avatarCanvas').innerHTML = '';
    
    // Recreate elements
    state.elements.forEach(elementData => {
        const element = createAdvancedElement({
            content: elementData.isImage ? 
                elementData.content.match(/url\(["']?([^"']*)["']?\)/)?.[1] :
                elementData.content,
            x: elementData.position.x,
            y: elementData.position.y,
            size: elementData.size.width,
            opacity: elementData.opacity,
            zIndex: elementData.zIndex,
            isImage: elementData.isImage
        });
        
        // Apply transform
        if (elementData.transform) {
            element.style.transform = elementData.transform;
        }
    });
    
    return true;
}
```

### 5. Export Customization

#### Custom Export Formats
```javascript
// Export as different sizes
async function exportCustomSize(width, height) {
    const canvas = document.getElementById('avatarCanvas');
    const originalWidth = canvas.style.width;
    const originalHeight = canvas.style.height;
    
    // Temporarily resize
    canvas.style.width = width + 'px';
    canvas.style.height = height + 'px';
    
    // Export
    const dataUrl = await domtoimage.toPng(canvas, {
        width: width,
        height: height
    });
    
    // Restore original size
    canvas.style.width = originalWidth;
    canvas.style.height = originalHeight;
    
    return dataUrl;
}

// Usage
exportCustomSize(1024, 1024).then(dataUrl => {
    const link = document.createElement('a');
    link.download = 'avatar-1024x1024.png';
    link.href = dataUrl;
    link.click();
});
```

#### Export with Background
```javascript
async function exportWithBackground(backgroundColor = '#ffffff') {
    const canvas = document.getElementById('avatarCanvas');
    
    return await domtoimage.toPng(canvas, {
        bgcolor: backgroundColor,
        width: canvas.offsetWidth,
        height: canvas.offsetHeight
    });
}

// Usage
exportWithBackground('#000000').then(dataUrl => {
    const link = document.createElement('a');
    link.download = 'avatar-black-bg.png';
    link.href = dataUrl;
    link.click();
});
```

---

## Workflow Examples

### 1. Creating a Profile Avatar

```javascript
// Step-by-step profile avatar creation
async function createProfileAvatar() {
    // 1. Upload base image
    console.log('Step 1: Upload your photo...');
    uploadImage(); // User selects photo
    
    // Wait for upload (in real scenario, use event listeners)
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    // 2. Add decorative elements
    console.log('Step 2: Adding decorative elements...');
    addIcon('✨'); // Sparkles
    addIcon('🎉'); // Party
    
    // 3. Position elements
    setTimeout(() => {
        const elements = document.querySelectorAll('.draggable');
        if (elements.length >= 2) {
            // Position sparkles top-left
            elements[0].style.left = '50px';
            elements[0].style.top = '50px';
            elements[0].style.opacity = '0.8';
            
            // Position party bottom-right
            elements[1].style.left = '400px';
            elements[1].style.top = '400px';
            elements[1].style.opacity = '0.7';
        }
    }, 500);
    
    // 4. Final adjustments
    setTimeout(() => {
        console.log('Step 3: Final adjustments...');
        // Make elements slightly smaller
        document.querySelectorAll('.draggable').forEach(el => {
            if (el.textContent) { // Only emoji elements
                selectElement(el);
                updateSelectedSize(40);
            }
        });
    }, 1000);
    
    console.log('Profile avatar ready! Click Download to save.');
}
```

### 2. Creating a Gaming Avatar

```javascript
async function createGamingAvatar() {
    console.log('Creating gaming avatar...');
    
    // Gaming-themed elements
    const gamingEmojis = ['🎮', '🎯', '⚡', '🔥', '💎', '👾', '🚀'];
    
    // Add random gaming elements
    for (let i = 0; i < 5; i++) {
        const randomEmoji = gamingEmojis[Math.floor(Math.random() * gamingEmojis.length)];
        addIcon(randomEmoji);
        
        // Random positioning
        setTimeout(() => {
            const elements = document.querySelectorAll('.draggable');
            const lastElement = elements[elements.length - 1];
            if (lastElement) {
                lastElement.style.left = Math.random() * 400 + 'px';
                lastElement.style.top = Math.random() * 400 + 'px';
                lastElement.style.transform = `rotate(${Math.random() * 360}deg)`;
            }
        }, i * 200);
    }
    
    // Add glow effects
    setTimeout(() => {
        document.querySelectorAll('.draggable').forEach(el => {
            el.style.filter = 'drop-shadow(0 0 10px #00f7ff)';
        });
    }, 1500);
    
    console.log('Gaming avatar created!');
}
```

### 3. Creating a Business Avatar

```javascript
function createBusinessAvatar() {
    console.log('Creating professional business avatar...');
    
    // Professional elements
    const businessEmojis = ['💼', '📊', '💰', '🏆', '⭐', '💎'];
    
    // Add subtle professional elements
    businessEmojis.slice(0, 3).forEach((emoji, index) => {
        addIcon(emoji);
        
        setTimeout(() => {
            const elements = document.querySelectorAll('.draggable');
            const element = elements[elements.length - 1];
            if (element) {
                // Position in corners
                const positions = [
                    { x: 50, y: 50 },    // Top-left
                    { x: 400, y: 50 },   // Top-right
                    { x: 400, y: 400 }   // Bottom-right
                ];
                
                element.style.left = positions[index].x + 'px';
                element.style.top = positions[index].y + 'px';
                element.style.opacity = '0.6'; // Subtle
                updateSelectedSize(30); // Small size
            }
        }, index * 300);
    });
    
    console.log('Business avatar elements added!');
}
```

---

## Tips & Tricks

### 1. Keyboard Shortcuts

```javascript
// Add keyboard shortcuts for common operations
document.addEventListener('keydown', (e) => {
    if (!selectedElement) return;
    
    switch(e.key) {
        case 'Delete':
        case 'Backspace':
            deleteSelected();
            break;
        case 'ArrowUp':
            e.preventDefault();
            selectedElement.style.top = (parseInt(selectedElement.style.top) - 5) + 'px';
            break;
        case 'ArrowDown':
            e.preventDefault();
            selectedElement.style.top = (parseInt(selectedElement.style.top) + 5) + 'px';
            break;
        case 'ArrowLeft':
            e.preventDefault();
            selectedElement.style.left = (parseInt(selectedElement.style.left) - 5) + 'px';
            break;
        case 'ArrowRight':
            e.preventDefault();
            selectedElement.style.left = (parseInt(selectedElement.style.left) + 5) + 'px';
            break;
        case '+':
        case '=':
            e.preventDefault();
            const currentSize = parseInt(selectedElement.style.width) || 60;
            updateSelectedSize(Math.min(500, currentSize + 10));
            break;
        case '-':
            e.preventDefault();
            const currentSize2 = parseInt(selectedElement.style.width) || 60;
            updateSelectedSize(Math.max(10, currentSize2 - 10));
            break;
    }
});
```

### 2. Snap to Grid

```javascript
// Enable snap-to-grid functionality
function enableSnapToGrid(gridSize = 20) {
    // Override the drag function to snap positions
    const originalSetupInteractions = setupElementInteractions;
    
    window.setupElementInteractions = function(element) {
        originalSetupInteractions(element);
        
        // Add snap functionality to drag end
        element.addEventListener('mouseup', () => {
            const x = parseInt(element.style.left);
            const y = parseInt(element.style.top);
            
            const snappedX = Math.round(x / gridSize) * gridSize;
            const snappedY = Math.round(y / gridSize) * gridSize;
            
            element.style.left = snappedX + 'px';
            element.style.top = snappedY + 'px';
        });
    };
}

// Usage
enableSnapToGrid(25); // Snap to 25px grid
```

### 3. Auto-Save Functionality

```javascript
// Auto-save avatar state every 30 seconds
function enableAutoSave(intervalSeconds = 30) {
    setInterval(() => {
        const state = saveAvatarState();
        console.log('Auto-saved avatar state:', state.timestamp);
        
        // Show temporary notification
        showNotification('Avatar auto-saved!', 2000);
    }, intervalSeconds * 1000);
}

function showNotification(message, duration = 3000) {
    const notification = document.createElement('div');
    notification.textContent = message;
    notification.style.cssText = `
        position: fixed;
        top: 20px;
        right: 20px;
        background: rgba(0, 247, 255, 0.9);
        color: #0a0a1a;
        padding: 10px 20px;
        border-radius: 20px;
        z-index: 1000;
        font-weight: 600;
        transition: all 0.3s ease;
    `;
    
    document.body.appendChild(notification);
    
    setTimeout(() => {
        notification.style.opacity = '0';
        notification.style.transform = 'translateX(100px)';
        setTimeout(() => notification.remove(), 300);
    }, duration);
}

// Enable auto-save
enableAutoSave(30);
```

### 4. Element Grouping

```javascript
// Group multiple elements together
class ElementGroup {
    constructor(elements) {
        this.elements = elements;
        this.groupId = 'group-' + Date.now();
    }
    
    move(deltaX, deltaY) {
        this.elements.forEach(element => {
            const currentX = parseInt(element.style.left) || 0;
            const currentY = parseInt(element.style.top) || 0;
            element.style.left = (currentX + deltaX) + 'px';
            element.style.top = (currentY + deltaY) + 'px';
        });
    }
    
    rotate(angle) {
        this.elements.forEach(element => {
            const currentTransform = element.style.transform || '';
            const withoutRotate = currentTransform.replace(/rotate\([^)]*\)/g, '').trim();
            const newTransform = withoutRotate ? 
                `${withoutRotate} rotate(${angle}deg)` : 
                `rotate(${angle}deg)`;
            element.style.transform = newTransform;
        });
    }
    
    scale(factor) {
        this.elements.forEach(element => {
            const currentWidth = parseInt(element.style.width) || 60;
            const currentHeight = parseInt(element.style.height) || 60;
            const newWidth = currentWidth * factor;
            const newHeight = currentHeight * factor;
            
            element.style.width = newWidth + 'px';
            element.style.height = newHeight + 'px';
            
            if (element.textContent) {
                element.style.fontSize = newWidth + 'px';
            }
        });
    }
}

// Usage
const selectedElements = document.querySelectorAll('.draggable.selected');
const group = new ElementGroup(Array.from(selectedElements));
group.move(50, 50);     // Move group 50px right and down
group.rotate(45);       // Rotate all elements 45 degrees
group.scale(1.2);       // Scale all elements by 120%
```

### 5. Template System

```javascript
// Create and use avatar templates
const avatarTemplates = {
    party: {
        name: 'Party Avatar',
        elements: [
            { content: '🎉', x: 100, y: 100, size: 60 },
            { content: '🎊', x: 300, y: 150, size: 50 },
            { content: '✨', x: 200, y: 300, size: 40 },
            { content: '🎈', x: 350, y: 300, size: 55 }
        ]
    },
    
    professional: {
        name: 'Professional Avatar',
        elements: [
            { content: '💼', x: 50, y: 50, size: 30, opacity: 0.7 },
            { content: '📊', x: 400, y: 50, size: 30, opacity: 0.7 },
            { content: '🏆', x: 400, y: 400, size: 30, opacity: 0.7 }
        ]
    },
    
    gaming: {
        name: 'Gaming Avatar',
        elements: [
            { content: '🎮', x: 150, y: 100, size: 70, rotation: 15 },
            { content: '⚡', x: 300, y: 200, size: 50, rotation: -20 },
            { content: '🔥', x: 200, y: 350, size: 60, rotation: 30 }
        ]
    }
};

function applyTemplate(templateName) {
    const template = avatarTemplates[templateName];
    if (!template) {
        console.error('Template not found:', templateName);
        return;
    }
    
    // Clear existing elements
    document.querySelectorAll('.draggable').forEach(el => el.remove());
    
    // Apply template elements
    template.elements.forEach((elementData, index) => {
        setTimeout(() => {
            const element = createAdvancedElement(elementData);
            console.log(`Added ${elementData.content} from ${template.name} template`);
        }, index * 200);
    });
    
    console.log(`Applied template: ${template.name}`);
}

// Usage
applyTemplate('party');        // Apply party template
applyTemplate('professional'); // Apply professional template
applyTemplate('gaming');       // Apply gaming template
```

---

## Troubleshooting

### Common Issues and Solutions

#### 1. Elements Not Appearing
```javascript
// Problem: Added elements don't show up
// Solution: Check if canvas exists and element is properly created

function debugAddIcon(icon) {
    console.log('Adding icon:', icon);
    
    const canvas = document.getElementById('avatarCanvas');
    if (!canvas) {
        console.error('Canvas not found!');
        return;
    }
    
    addIcon(icon);
    
    // Verify element was added
    setTimeout(() => {
        const elements = canvas.querySelectorAll('.draggable');
        console.log('Total elements on canvas:', elements.length);
        console.log('Last element:', elements[elements.length - 1]);
    }, 100);
}
```

#### 2. Control Panel Not Showing
```javascript
// Problem: Control panel doesn't appear when element is selected
// Solution: Check element selection and panel state

function debugSelection(element) {
    console.log('Selecting element:', element);
    console.log('Element has selected class:', element.classList.contains('selected'));
    
    selectElement(element);
    
    const panel = document.getElementById('controlPanel');
    console.log('Control panel active:', panel.classList.contains('active'));
    console.log('Control panel display:', window.getComputedStyle(panel).display);
}
```

#### 3. Download Not Working
```javascript
// Problem: Download button doesn't work
// Solution: Check export libraries and fallback methods

function debugDownload() {
    console.log('Testing download functionality...');
    
    // Check if libraries are loaded
    console.log('html2canvas available:', typeof html2canvas !== 'undefined');
    console.log('domtoimage available:', typeof domtoimage !== 'undefined');
    
    // Test canvas content
    const canvas = document.getElementById('avatarCanvas');
    const elements = canvas.querySelectorAll('.draggable');
    console.log('Elements to export:', elements.length);
    
    if (elements.length === 0) {
        console.warn('No elements to export! Add some elements first.');
        return;
    }
    
    // Try download
    downloadAvatar();
}
```

#### 4. Performance Issues
```javascript
// Problem: App becomes slow with many elements
// Solution: Optimize rendering and event handling

function optimizePerformance() {
    // Limit maximum elements
    const MAX_ELEMENTS = 50;
    
    const originalAddIcon = addIcon;
    window.addIcon = function(icon) {
        const currentElements = document.querySelectorAll('.draggable').length;
        if (currentElements >= MAX_ELEMENTS) {
            showNotification(`Maximum ${MAX_ELEMENTS} elements allowed!`, 3000);
            return;
        }
        originalAddIcon(icon);
    };
    
    // Debounce slider updates
    function debounce(func, wait) {
        let timeout;
        return function executedFunction(...args) {
            const later = () => {
                clearTimeout(timeout);
                func(...args);
            };
            clearTimeout(timeout);
            timeout = setTimeout(later, wait);
        };
    }
    
    // Apply debouncing to slider functions
    window.updateSelectedSize = debounce(updateSelectedSize, 50);
    window.updateSelectedRotation = debounce(updateSelectedRotation, 50);
    window.updateSelectedOpacity = debounce(updateSelectedOpacity, 50);
}
```

---

## Best Practices

### 1. Layer Management

```javascript
// Best practice: Organize elements by layers
const LAYER_LEVELS = {
    BACKGROUND: 1,
    BASE_ELEMENTS: 10,
    DECORATIONS: 20,
    EFFECTS: 30,
    FOREGROUND: 40
};

function setElementLayer(element, layer) {
    element.style.zIndex = layer;
    element.dataset.layer = layer;
}

// Usage
addIcon('🎨'); // Add background decoration
setTimeout(() => {
    const element = document.querySelector('.draggable:last-child');
    setElementLayer(element, LAYER_LEVELS.BACKGROUND);
}, 100);
```

### 2. Consistent Sizing

```javascript
// Best practice: Use consistent size ratios
const SIZE_PRESETS = {
    TINY: 20,
    SMALL: 40,
    MEDIUM: 60,
    LARGE: 80,
    HUGE: 120
};

function setStandardSize(element, sizeKey) {
    const size = SIZE_PRESETS[sizeKey];
    if (size) {
        selectElement(element);
        updateSelectedSize(size);
    }
}
```

### 3. Color Coordination

```javascript
// Best practice: Apply consistent color themes
function applyColorTheme(theme) {
    const themes = {
        warm: {
            filter: 'hue-rotate(30deg) saturate(1.2)',
            elements: ['🔥', '☀️', '🌅', '🧡', '❤️']
        },
        cool: {
            filter: 'hue-rotate(180deg) saturate(1.1)',
            elements: ['❄️', '🌊', '💙', '💎', '⭐']
        },
        nature: {
            filter: 'hue-rotate(90deg) saturate(1.3)',
            elements: ['🌿', '🌸', '🦋', '🌈', '🍃']
        }
    };
    
    const selectedTheme = themes[theme];
    if (selectedTheme) {
        document.querySelectorAll('.draggable').forEach(el => {
            el.style.filter = selectedTheme.filter;
        });
    }
}
```

### 4. Responsive Design

```javascript
// Best practice: Make avatars work on different screen sizes
function makeResponsive() {
    function adjustForScreenSize() {
        const canvas = document.getElementById('avatarCanvas');
        const screenWidth = window.innerWidth;
        
        if (screenWidth < 640) {
            // Mobile adjustments
            canvas.style.width = '300px';
            canvas.style.height = '300px';
            
            // Scale down all elements
            document.querySelectorAll('.draggable').forEach(el => {
                const currentSize = parseInt(el.style.width) || 60;
                const newSize = Math.max(20, currentSize * 0.7);
                el.style.width = newSize + 'px';
                el.style.height = newSize + 'px';
                if (el.textContent) {
                    el.style.fontSize = newSize + 'px';
                }
            });
        }
    }
    
    // Adjust on load and resize
    adjustForScreenSize();
    window.addEventListener('resize', adjustForScreenSize);
}
```

### 5. Accessibility

```javascript
// Best practice: Add accessibility features
function enhanceAccessibility() {
    // Add ARIA labels
    document.querySelectorAll('.draggable').forEach((el, index) => {
        el.setAttribute('role', 'button');
        el.setAttribute('aria-label', `Avatar element ${index + 1}: ${el.textContent || 'image'}`);
        el.setAttribute('tabindex', '0');
        
        // Keyboard navigation
        el.addEventListener('keydown', (e) => {
            if (e.key === 'Enter' || e.key === ' ') {
                e.preventDefault();
                selectElement(el);
            }
        });
    });
    
    // Add focus indicators
    const style = document.createElement('style');
    style.textContent = `
        .draggable:focus {
            outline: 2px solid #00f7ff;
            outline-offset: 2px;
        }
    `;
    document.head.appendChild(style);
}
```

---

This comprehensive usage guide provides everything needed to effectively use the IRYS Avatar Creator, from basic operations to advanced techniques and best practices. Whether you're a beginner or an advanced user, these examples and workflows will help you create amazing avatars efficiently.