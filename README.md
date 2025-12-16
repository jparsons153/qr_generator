# QR Code Generator

A simple and elegant QR code generator built with Vue 3 and Vite. Enter any URL and instantly generate a downloadable QR code.

## Features

- Clean, modern user interface
- Instant QR code generation
- Download QR codes as PNG files
- Input validation
- Responsive design
- Keyboard shortcuts (press Enter to generate)

## Tech Stack

- **Vue 3** - Progressive JavaScript framework
- **Vite** - Fast build tool and dev server
- **qrcode** - QR code generation library

## Getting Started

### Prerequisites

- Node 24

### Installation

1. Clone or download this repository

2. Install dependencies:
```bash
npm install
```

### Development

Start the development server:
```bash
npm run dev
```

The app will be available at `http://localhost:5173` 

### Build for Production

Create an optimized production build:
```bash
npm run build
```

The built files will be in the `dist` directory.

### Preview Production Build

Preview the production build locally:
```bash
npm run preview
```

## Usage

1. Enter a URL in the input field
2. Click "Generate QR Code" or press Enter
3. The QR code will appear on the screen
4. Click "Download PNG" to save the QR code to your computer

## Project Structure

```
qr_generator/
├── package.json              # Project dependencies and scripts
├── vite.config.js           # Vite configuration
├── index.html               # HTML entry point
└── src/
    ├── main.js              # Vue app initialization
    ├── App.vue              # Main QR generator component
    └── style.css            # Global styles
```

## Customization

### QR Code Options

You can customize the QR code generation in `src/App.vue`:

```javascript
const dataUrl = await QRCode.toDataURL(url.value, {
  width: 256,        // Change size
  margin: 2,         // Change margin
  color: {
    dark: '#000000', // Change QR code color
    light: '#ffffff' // Change background color
  }
})
```

### Styling

- Global styles: `src/style.css`
- Component styles: `<style scoped>` section in `src/App.vue`

## License

MIT
