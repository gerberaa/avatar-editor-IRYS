# 🎨 IRYS Avatar Creator - API Documentation

## Table of Contents

1. [Overview](#overview)
2. [Core Components](#core-components)
3. [Public APIs](#public-apis)
4. [Event Handlers](#event-handlers)
5. [UI Components](#ui-components)
6. [Usage Examples](#usage-examples)
7. [Integration Guide](#integration-guide)

## Overview

The IRYS Avatar Creator is a modern web application built with HTML5, CSS3, and vanilla JavaScript. It provides a comprehensive avatar editing experience with drag-and-drop functionality, real-time editing controls, and export capabilities.

### Key Features
- **Canvas-based editing** with draggable elements
- **Multi-category content** (emojis, accessories, custom uploads)
- **Real-time element manipulation** (resize, rotate, opacity, layering)
- **Export functionality** with multiple fallback methods
- **Responsive design** with animated backgrounds
- **Interactive help system**

---

## Core Components

### 1. Avatar Canvas
The main editing area where users create their avatars.

**HTML Element:** `#avatarCanvas`
**Dimensions:** 500x500px
**Features:**
- Drag-and-drop element placement
- Element selection and manipulation
- Background gradient with animated border
- Hover effects and visual feedback

### 2. Category System
Three main content categories for avatar elements.

#### Emojis Panel (`#emojiPanel`)
- **Content:** 200+ emoji characters
- **Layout:** 8-column grid
- **Usage:** Click to add emoji to canvas

#### Accessories Panel (`#accessoryPanel`)
- **Content:** 50+ accessory emojis (hats, glasses, jewelry)
- **Layout:** 6-column grid
- **Usage:** Click to add accessory to canvas

#### Personal Panel (`#personalPanel`)
- **Content:** User-uploaded custom images
- **Layout:** 4-column grid
- **Features:** Upload, preview, delete custom items

### 3. Control Panel
Real-time element editing interface that appears when an element is selected.

**Location:** Fixed right side of screen
**Controls:**
- Size slider (1-500px)
- Rotation slider (0-360°)
- Opacity slider (0-100%)
- Z-index slider (1-100)
- Delete button

---

## Public APIs

### Core Functions

#### `initializeCategories()`
Initializes all content categories and populates them with items.

```javascript
function initializeCategories()
```

**Usage:**
- Called automatically on page load
- Populates emoji and accessory panels
- Sets up initial UI state

**Example:**
```javascript
// Manually reinitialize categories
initializeCategories();
```

---

#### `uploadImage()`
Triggers the base avatar image upload dialog.

```javascript
function uploadImage()
```

**Usage:**
- Opens file picker for JPG/PNG images
- Adds uploaded image as background element
- Supports drag-and-drop manipulation

**Example:**
```javascript
// Programmatically trigger upload
uploadImage();
```

---

#### `addIcon(icon)`
Adds an emoji or text element to the canvas.

```javascript
function addIcon(icon)
```

**Parameters:**
- `icon` (string): The emoji or text character to add

**Features:**
- Creates draggable element at position (100px, 100px)
- Default size: 60px
- Includes rotation and resize handles
- Auto-assigns unique ID

**Example:**
```javascript
// Add specific emojis
addIcon('😀');
addIcon('👑');
addIcon('🎉');
```

---

#### `downloadAvatar()`
Exports the current avatar as a PNG image.

```javascript
function downloadAvatar()
```

**Features:**
- Multiple export methods (html2canvas, dom-to-image, manual canvas)
- Automatic fallback system
- Hides UI elements during export
- 2x scale for high quality

**Example:**
```javascript
// Download current avatar
downloadAvatar();
```

---

### Element Manipulation Functions

#### `selectElement(element)`
Selects an element and shows the control panel.

```javascript
function selectElement(element)
```

**Parameters:**
- `element` (HTMLElement): The element to select

**Effects:**
- Highlights selected element
- Shows control panel
- Updates sliders with current values

**Example:**
```javascript
// Select first draggable element
const firstElement = document.querySelector('.draggable');
selectElement(firstElement);
```

---

#### `updateSelectedSize(value)`
Updates the size of the currently selected element.

```javascript
function updateSelectedSize(value)
```

**Parameters:**
- `value` (number): New size in pixels (1-500)

**Example:**
```javascript
// Make selected element 100px
updateSelectedSize(100);
```

---

#### `updateSelectedRotation(value)`
Rotates the currently selected element.

```javascript
function updateSelectedRotation(value)
```

**Parameters:**
- `value` (number): Rotation angle in degrees (0-360)

**Example:**
```javascript
// Rotate selected element 45 degrees
updateSelectedRotation(45);
```

---

#### `updateSelectedOpacity(value)`
Changes the opacity of the currently selected element.

```javascript
function updateSelectedOpacity(value)
```

**Parameters:**
- `value` (number): Opacity percentage (0-100)

**Example:**
```javascript
// Make selected element 50% transparent
updateSelectedOpacity(50);
```

---

#### `updateSelectedZIndex(value)`
Changes the layer order of the currently selected element.

```javascript
function updateSelectedZIndex(value)
```

**Parameters:**
- `value` (number): Z-index value (1-100)

**Example:**
```javascript
// Bring selected element to front
updateSelectedZIndex(100);
```

---

#### `deleteSelected()`
Removes the currently selected element from the canvas.

```javascript
function deleteSelected()
```

**Example:**
```javascript
// Delete currently selected element
deleteSelected();
```

---

### Category Management

#### `showCategory(category)`
Switches between content categories.

```javascript
function showCategory(category)
```

**Parameters:**
- `category` (string): 'emojis', 'accessories', or 'personal'

**Effects:**
- Updates active tab styling
- Shows corresponding content panel
- Hides other panels

**Example:**
```javascript
// Show accessories category
showCategory('accessories');

// Show custom uploads
showCategory('personal');
```

---

#### `populateEmojis()`
Populates the emoji panel with available emojis.

```javascript
function populateEmojis()
```

**Data Source:** `emojiCollection` array (200+ emojis)

---

#### `populateAccessories()`
Populates the accessories panel with available items.

```javascript
function populateAccessories()
```

**Data Source:** `accessoryCollection` array (50+ accessories)

---

### Custom Content Management

#### `uploadPersonalItem()`
Triggers upload dialog for custom images.

```javascript
function uploadPersonalItem()
```

**Supported Formats:** JPG, PNG, GIF, WebP
**Storage:** Session-based (clears on page reload)

---

#### `addPersonalToCanvas(imageSrc)`
Adds a custom uploaded image to the canvas.

```javascript
function addPersonalToCanvas(imageSrc)
```

**Parameters:**
- `imageSrc` (string): Data URL or image source

**Example:**
```javascript
// Add custom image (assuming you have the data URL)
addPersonalToCanvas('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...');
```

---

#### `deletePersonalItem(itemId)`
Removes a custom item from the personal collection.

```javascript
function deletePersonalItem(itemId)
```

**Parameters:**
- `itemId` (string): Unique identifier for the personal item

---

### Utility Functions

#### `createParticles()`
Creates animated background particles.

```javascript
function createParticles()
```

**Features:**
- Creates 30 floating particles
- Random positioning and timing
- Continuous animation loop

---

#### `toggleHelp()`
Shows/hides the help modal.

```javascript
function toggleHelp()
```

**Example:**
```javascript
// Show help dialog
toggleHelp();
```

---

## Event Handlers

### File Upload Handlers

#### `handleFileUpload(event)`
Processes base avatar image uploads.

```javascript
function handleFileUpload(event)
```

**Triggered by:** File input change event
**Processes:** JPG, PNG image files
**Action:** Adds image to canvas as draggable element

---

#### `handlePersonalUpload(event)`
Processes custom item uploads.

```javascript
function handlePersonalUpload(event)
```

**Triggered by:** Personal file input change event
**Action:** Adds image to personal collection grid

---

### Element Interaction Handlers

#### `setupElementInteractions(element)`
Sets up all interaction handlers for a canvas element.

```javascript
function setupElementInteractions(element)
```

**Parameters:**
- `element` (HTMLElement): The element to set up

**Interactions Added:**
- Click to select
- Drag to move
- Rotate handle interaction
- Resize handle interaction

---

## UI Components

### Button Components

#### Upload Button
```html
<button class="btn" onclick="uploadImage()">Upload Avatar</button>
```
**Purpose:** Trigger base image upload
**Styling:** Primary button with gradient background

#### Download Button
```html
<button class="btn-download btn" onclick="downloadAvatar()">Download</button>
```
**Purpose:** Export avatar as PNG
**Styling:** Download-specific styling with icon

#### Category Tabs
```html
<button class="category-tab active" onclick="showCategory('emojis')" data-category="emojis">
    😀 Emojis
</button>
```
**Purpose:** Switch between content categories
**States:** Active/inactive styling

### Interactive Elements

#### Emoji Items
```html
<div class="emoji-item" onclick="addIcon('😀')">😀</div>
```
**Purpose:** Add emoji to canvas
**Interaction:** Click to add

#### Personal Items
```html
<div class="personal-item">
    <img src="..." alt="...">
    <button class="delete-btn" onclick="deletePersonalItem('id')">&times;</button>
</div>
```
**Purpose:** Display and manage custom uploads
**Interactions:** Click to add, delete button to remove

### Control Elements

#### Sliders
```html
<input type="range" id="sizeSlider" min="1" max="500" value="60" 
       oninput="updateSelectedSize(this.value)">
```
**Types:** Size, Rotation, Opacity, Z-Index
**Real-time:** Updates element properties immediately

---

## Usage Examples

### Basic Avatar Creation

```javascript
// 1. Initialize the application
initializeCategories();

// 2. Add a base image
uploadImage(); // User selects file

// 3. Add some emojis
addIcon('😀');
addIcon('👑');
addIcon('🎉');

// 4. Select and modify an element
const element = document.querySelector('.draggable');
selectElement(element);
updateSelectedSize(80);
updateSelectedRotation(15);
updateSelectedOpacity(90);

// 5. Download the result
downloadAvatar();
```

### Programmatic Element Creation

```javascript
// Create a custom element programmatically
function createCustomElement(content, x, y, size) {
    const canvas = document.getElementById('avatarCanvas');
    const element = document.createElement('div');
    
    element.className = 'draggable';
    element.style.position = 'absolute';
    element.style.left = x + 'px';
    element.style.top = y + 'px';
    element.style.fontSize = size + 'px';
    element.style.width = size + 'px';
    element.style.height = size + 'px';
    element.textContent = content;
    element.id = 'element-' + Date.now();
    
    // Add control handles
    const rotateHandle = document.createElement('div');
    rotateHandle.className = 'rotate-handle';
    element.appendChild(rotateHandle);
    
    const resizeHandle = document.createElement('div');
    resizeHandle.className = 'resize-handle';
    element.appendChild(resizeHandle);
    
    setupElementInteractions(element);
    canvas.appendChild(element);
    
    return element;
}

// Usage
const customElement = createCustomElement('🚀', 200, 150, 80);
```

### Category Management

```javascript
// Switch to accessories and add items
showCategory('accessories');
setTimeout(() => {
    addIcon('👑');
    addIcon('🕶️');
    addIcon('💎');
}, 100);

// Switch to custom uploads
showCategory('personal');
uploadPersonalItem(); // User uploads custom image
```

### Batch Element Operations

```javascript
// Select all elements and apply transformations
const elements = document.querySelectorAll('.draggable');
elements.forEach((element, index) => {
    selectElement(element);
    updateSelectedRotation(index * 45); // Rotate each by different amount
    updateSelectedOpacity(80); // Make all semi-transparent
});
```

---

## Integration Guide

### Embedding in Your Application

1. **Include Required Dependencies:**
```html
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/dom-to-image/2.6.0/dom-to-image.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
```

2. **Initialize the Application:**
```javascript
document.addEventListener('DOMContentLoaded', () => {
    initializeCategories();
    createParticles();
});
```

3. **Custom Event Listeners:**
```javascript
// Listen for element selection
document.addEventListener('elementSelected', (event) => {
    console.log('Element selected:', event.detail.element);
});

// Listen for avatar download
document.addEventListener('avatarDownloaded', (event) => {
    console.log('Avatar downloaded:', event.detail.filename);
});
```

### Customization Options

#### Modify Content Collections

```javascript
// Add custom emojis
const customEmojis = ['🎮', '🎯', '🎪', '🎭'];
emojiCollection.push(...customEmojis);
populateEmojis(); // Refresh the panel

// Add custom accessories
const customAccessories = ['🎩', '🥽', '🎀'];
accessoryCollection.push(...customAccessories);
populateAccessories(); // Refresh the panel
```

#### Custom Styling

```css
/* Override default canvas size */
.avatar-canvas {
    width: 600px;
    height: 600px;
}

/* Custom button styling */
.btn {
    background: linear-gradient(135deg, #your-color, #your-color-dark);
}

/* Custom element styling */
.draggable.selected {
    border-color: #your-accent-color;
    box-shadow: 0 0 10px rgba(your-accent-color, 0.5);
}
```

#### API Extensions

```javascript
// Extend functionality with custom methods
window.AvatarCreator = {
    // Save avatar state
    saveState: function() {
        const elements = Array.from(document.querySelectorAll('.draggable'));
        return elements.map(el => ({
            id: el.id,
            content: el.textContent || el.style.backgroundImage,
            style: {
                left: el.style.left,
                top: el.style.top,
                width: el.style.width,
                height: el.style.height,
                transform: el.style.transform,
                opacity: el.style.opacity,
                zIndex: el.style.zIndex
            }
        }));
    },
    
    // Load avatar state
    loadState: function(state) {
        // Clear current canvas
        document.getElementById('avatarCanvas').innerHTML = '';
        
        // Recreate elements
        state.forEach(elementData => {
            if (elementData.content.startsWith('url(')) {
                // Handle image elements
                addPersonalToCanvas(elementData.content);
            } else {
                // Handle text/emoji elements
                addIcon(elementData.content);
            }
            
            // Apply saved styles
            const element = document.getElementById(elementData.id);
            if (element) {
                Object.assign(element.style, elementData.style);
            }
        });
    },
    
    // Export as different formats
    exportAs: function(format = 'png') {
        const canvas = document.getElementById('avatarCanvas');
        switch (format) {
            case 'jpg':
                return domtoimage.toJpeg(canvas);
            case 'svg':
                return domtoimage.toSvg(canvas);
            case 'blob':
                return domtoimage.toBlob(canvas);
            default:
                return domtoimage.toPng(canvas);
        }
    }
};
```

### Performance Optimization

#### Lazy Loading
```javascript
// Lazy load emoji collections
const lazyLoadEmojis = () => {
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                populateEmojis();
                observer.unobserve(entry.target);
            }
        });
    });
    
    observer.observe(document.getElementById('emojiPanel'));
};
```

#### Memory Management
```javascript
// Clean up event listeners when elements are removed
const cleanupElement = (element) => {
    element.removeEventListener('click', selectElement);
    element.removeEventListener('mousedown', /* drag handler */);
    // Remove other listeners...
};
```

---

## Browser Compatibility

**Supported Browsers:**
- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

**Required Features:**
- ES6 JavaScript
- CSS Grid
- CSS Custom Properties
- File API
- Canvas API

**Fallbacks Provided:**
- Multiple export methods
- Progressive enhancement
- Graceful degradation

---

## Error Handling

The application includes comprehensive error handling:

```javascript
// File upload errors
function handleUploadError(error) {
    console.error('Upload failed:', error);
    // Show user-friendly message
}

// Export errors
function handleExportError(error) {
    console.error('Export failed:', error);
    // Try fallback method
    manualCanvasDownload();
}

// Element manipulation errors
function handleElementError(error) {
    console.error('Element error:', error);
    // Reset element state
}
```

---

## Security Considerations

- **File Upload Validation:** Only accepts image files
- **XSS Prevention:** Sanitizes user input
- **CORS Handling:** Proper cross-origin image handling
- **Memory Limits:** Prevents excessive resource usage

---

This documentation covers all public APIs and components of the IRYS Avatar Creator. For additional support or feature requests, please refer to the project repository or contact the development team.