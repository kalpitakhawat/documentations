# Portals and Modals in React

## Introduction

React Portals provide a way to render components outside the main DOM hierarchy while maintaining the React tree's structure and context. This feature is particularly useful for implementing modals, overlays, tooltips, and other UI elements that need to be rendered at a different location in the DOM.

This guide explores how to use React Portals and best practices for creating modals and overlays.

## What are React Portals?

React Portals allow you to render children into a DOM node that exists outside the hierarchy of the parent component.

### Creating a Portal

1. **Create a DOM Node**: Add a container for the portal in your HTML file.

```html
<!-- public/index.html -->
<div id="portal-root"></div>
```

2. **Use `ReactDOM.createPortal`**: Render the child component into the specified DOM node.

```javascript
import ReactDOM from 'react-dom';

function Modal({ children }) {
  const portalRoot = document.getElementById('portal-root');
  return ReactDOM.createPortal(
    <div className="modal">
      {children}
    </div>,
    portalRoot
  );
}

export default Modal;
```

3. **Use the Modal Component**:

```javascript
function App() {
  return (
    <div className="App">
      <h1>Welcome to the App</h1>
      <Modal>
        <p>This is rendered in a Portal!</p>
      </Modal>
    </div>
  );
}
```

## Implementing Modals with Portals

### Example: Basic Modal

Here’s a basic example of a modal component:

```javascript
import React, { useState } from 'react';
import ReactDOM from 'react-dom';

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  return ReactDOM.createPortal(
    <div className="modal-overlay">
      <div className="modal-content">
        <button onClick={onClose} className="modal-close">X</button>
        {children}
      </div>
    </div>,
    document.getElementById('portal-root')
  );
}

export default function App() {
  const [isModalOpen, setModalOpen] = useState(false);

  return (
    <div className="App">
      <button onClick={() => setModalOpen(true)}>Open Modal</button>
      <Modal isOpen={isModalOpen} onClose={() => setModalOpen(false)}>
        <h2>Modal Title</h2>
        <p>This is a modal dialog.</p>
      </Modal>
    </div>
  );
}
```

### Styling the Modal

Add the following CSS to style the modal:

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.modal-close {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
}
```

## Best Practices for Portals and Modals

1. **Keyboard Accessibility**:
   - Use `tabIndex` and `aria-*` attributes to make modals accessible.
   - Trap focus within the modal and allow it to return to the triggering element when closed.

   ```javascript
   import { useEffect, useRef } from 'react';

   function Modal({ isOpen, onClose, children }) {
     const modalRef = useRef();

     useEffect(() => {
       if (isOpen) {
         modalRef.current.focus();
       }
     }, [isOpen]);

     return ReactDOM.createPortal(
       <div
         className="modal-overlay"
         tabIndex="-1"
         ref={modalRef}
         onKeyDown={(e) => {
           if (e.key === 'Escape') onClose();
         }}
       >
         <div className="modal-content">{children}</div>
       </div>,
       document.getElementById('portal-root')
     );
   }
   ```

2. **Avoid Memory Leaks**:
   - Ensure event listeners and other side effects are cleaned up when the modal is unmounted.

3. **Manage Z-Index Conflicts**:
   - Use a high `z-index` value for modals and overlays to avoid conflicts with other UI elements.

4. **Lazy Mounting**:
   - Render modals conditionally to avoid unnecessary DOM nodes when the modal is not in use.

## Conclusion

React Portals offer a powerful way to manage components that need to break out of the normal DOM hierarchy. When combined with best practices for accessibility and performance, they provide an excellent solution for creating modals, overlays, and similar UI elements.

## Official Documentation

- [React Portals](https://react.dev/reference/react-dom/createPortal)

