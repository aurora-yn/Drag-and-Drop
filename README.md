# Drag and Drop API

## Define which elements in the page are **draggable**
```
<div draggable="true">
  ...
</div>
```
   - Images, text selections and links are draggable by default
   - Transferring files: Drag files from the user computer inside the browser

## Drop into an element which must be valid **drop target**
To make an element a drop target, add **dragover** event and return false from it, or call preventDefault() on the event passed:
```
const el = document.querySelector('#drop-target)
el.addEventListener('dragover', event => {
  event.preventDefault()
})
```
### - The events on the draggable element are:
   - dragstart
   - drag
   - dragend
### - On the drop target:
   - dragenter
   - dragover
   - dragleave
   - drop
---

## Drag Event: **DataTransfer**
DataTransfer holds the data being dragged during a drag and drop operation and offers 5 properties:
   - dropEffect (Get the type of the drag and drop operation, set by the user through the use of modifier keys)
   - effectAllowed (Set the effect of the drag operation by setting the property in the dragstart event)
   - files
   - items (read only)
   - types (read only)

### *effectAllowed*
Options which set how the drop target should handle the dropped element:
   - none it shouldn’t be dropped
   - move it can be moved
   - copy it can be copied
   - link it can be linked
   - copyMove it can be copied or moved
   - copyLink it can be copied or linked
   - linkMove it can be moved or linked
   - all it can be copied, moved or linked (default)
```
element.addEventListener('dragstart', event => {
  event.dataTrasfer.effectAllowed = 'move'
})
```

### *dropEffect*
This property is not read only. We can edit it in a dragenter or dragover event:
   - none it shouldn’t be dropped
   - move it can be moved
   - copy it can be copied
   - link it can be linked
```
element.addEventListener('dragenter', event => {
  event.dataTrasfer.dropEffect = 'copy'
})
```

[DataTransfer Details on MDN](https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer)

---

## **dataTransfer.items**
can iterate using a loop and get access to each DataTransferItem object

2 read-only properties:
   - kind: the kind of the item being dragged. Returns a string containing file or string
   - type the MIME type of the item

2 methods:
   - getAsFile() returns a File object representing the data being dragged
   - getAsString() executes the callback function pasing a string object representing the data being dragged