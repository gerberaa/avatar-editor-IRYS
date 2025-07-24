# ✨ IRYS Avatar Editor

IRYS Avatar Editor is a modern web application for creating and editing avatars using emojis, accessories, and your own images. The app features a stylish interface, animations, and user-friendly functionality.

## Main Features

- **Upload Base Avatar**: Upload your own image (JPG, PNG) as the base for your avatar.
- **Add Emojis**: A large collection of emojis to decorate your avatar.
- **Accessories**: Add hats, glasses, jewelry, and other accessories.
- **Custom Images**: Upload your own images (stickers, logos, art) and use them on your avatar.
- **Element Editing**:
  - Move, resize, rotate, change opacity, and layer order for each element.
  - Remove elements from the canvas.
- **Save Result**: Download your finished avatar as a PNG file.
- **Drag-and-drop Support**: Intuitive element control on the canvas.
- **Animated Background**: 3D IRYS cube, floating particles, and Sparait mascot.
- **Detailed Help**: Built-in help with instructions and tips.
- **Social Links**: Buttons to X (Twitter), Discord, and the official website.

## How to Use

1. **Upload a base image** using the "Upload Avatar" button or start with a blank canvas.
2. **Add elements**:
   - Choose a category (emojis, accessories, custom).
   - Click an element to add it to the canvas.
3. **Edit elements**:
   - Click an element to select it.
   - Drag to move.
   - Use the orange handle to resize, the cyan handle to rotate.
   - Adjust size, rotation, opacity, and layer order via the control panel on the right.
   - Delete elements with the "Delete Element" button.
4. **Download your avatar** using the "Download" button.
5. **Use the help** ("?" button at the bottom left) to view instructions.

## Design Features

- **Dark neon color scheme** with gradients and glow effects.
- **3D animations**: Rotating cube with IRYS letters.
- **Sparait mascot**: Interactive character in the bottom left corner.
- **Responsive interface** for different screen sizes.
- **Tooltips** on button hover.

## Technical Details

- **HTML, CSS (Tailwind, custom styles), JavaScript**.
- No backend — everything works in the browser.
- Uses [dom-to-image](https://github.com/tsayen/dom-to-image) (or html2canvas, if connected) for image export.
- Custom images are stored in session memory (until page reload).
- Supports modern browsers.

## Getting Started

1. Copy the files to any directory.
2. Open `index.html` in your browser.

## License

MIT License (or specify your own)

---

**IRYS Avatar Editor** — create unique avatars easily and with fun! 