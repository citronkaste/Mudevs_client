# Individual Functions - Index

This folder contains detailed documentation for each Game Client Lua API function, organized by category.

Each function has its own page with practical examples, parameter descriptions, return values, and related functions.

## 📋 Index by Category

### 🖱️ Input & Mouse
- [IsMouseClicked](IsMouseClicked.md) - Checks if left button was clicked
- [IsMouseHeld](IsMouseHeld.md) - Checks if the left button is pressed
- [CheckMouseIn](CheckMouseIn.md) - Checks if the mouse is in a rectangular area
- [SetBlockInput](SetBlockInput.md) - Lock/unlock game input
- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Checks if key was pressed
- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Checks if the key has been released
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Checks if the key is being held
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Checks if the key is not pressed

### 🎨 Rendering & Graphics
- [EnableAlphaBlend](EnableAlphaBlend.md) - Enables standard alpha blending
- [EnableAlphaBlendMinus](EnableAlphaBlendMinus.md) - Enable subtrative alpha blending
- [DisableAlphaBlend](DisableAlphaBlend.md) - Disable alpha blending
- [DisableDepthTest](DisableDepthTest.md) - Disable depth test
- [EnableDepthMask](EnableDepthMask.md) - Enables written non-Z-buffer
- [DisableDepthMask](DisableDepthMask.md) - Disables writing to the Z-buffer
- [DisableTexture](DisableTexture.md) - Disables texturing
- [EnableLightMap](EnableLightMap.md) - Habilita lightmapping
- [BindTexture](BindTexture.md) - Links texture for rendering
- [LoadBitmap](LoadBitmap.md) - Load texture from file
- [RenderBitmap](RenderBitmap.md) - Renders 2D image with complete control
- [RenderImage](RenderImage.md) - Renders simplified 2D image
- [Color4f](Color4f.md) - Creates color based on float
- [RGBA](RGBA.md) - Creates standard RGBA color

### 📝 Text & UI
- [UIRenderText_SetFont](UIRenderText_SetFont.md) - Set font for text
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Set text color
- [UIRenderText_SetBgColor](UIRenderText_SetBgColor.md) - Set text background color
- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renders text on screen
- [RenderTipText](RenderTipText.md) - Renders tooltip style text
- [IsWriteInterfaceOpen](IsWriteInterfaceOpen.md) - Checks if the writing interface is open

### 👤 Object Management
- [GetCharacter](GetCharacter.md) - Gets character object
- [GetModel](GetModel.md) - Gets 3D model object

### 🎮 Bridge Functions (Hooks)
- [BridgeFunction_OnLoadInterface](BridgeFunction_OnLoadInterface.md) - When UI is initializing
- [BridgeFunction_OnInterfaceRender](BridgeFunction_OnInterfaceRender.md) - Critical rendering loop
- [BridgeFunction_OnPacketRecv](BridgeFunction_OnPacketRecv.md) - When package is received

## 📝 Documentation Format

Each function file follows a standardized format:

1. **Title**: Name of the function
2. **Signature**: How to call the function (syntax)
3. **Parameters**: Detailed description of each parameter
4. **Return**: What the function returns
5. **Examples**: Practical examples of use
6. **Notes**: Important information and considerations
7. **Related Functions**: Links to related functions

## 🔍 How to Use This Documentation

### Search for a Role

1. **By Category**: Browse the categories above to find related roles
2. **By name**: The files are named exactly like the functions (ex:`IsMouseClicked.md ` to ` IsMouseClicked`)
3. **Editor Search**: Use your editor search to find specific functions

### Navigation Structure

- Each function has its own page with complete documentation
- Use the "Related Functions" links at the end of each page to explore similar functions
- Consult the main documentation for systems overview

## 📚 Related Documentation

For more detailed information about the systems, see:

- [Main Documentation](../README.md) - Overview and complete index
- [Bridge Functions](../05-Bridge-Functions.md) - Sistema de hooks e callbacks
- [Rendering System](../06-Rendering-System.md) - Complete rendering system
- [Input System](../07-Input-System.md) - Input, mouse and keyboard
- [UI System](../08-UI-System.md) - User interface and text

---

**Source**: This documentation is based on `Api.md`- Official documentation of the Game Client Lua API.

