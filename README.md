# Cobblemon NPC Tools
## NPC and Dialogue Builder for Cobblemon NPC creation
### What it does:
**Node graph** — every page is a draggable node, arrows show how pages connect. Right-click the canvas to add pages
Live preview panel that uses the a close approximation to the  Cobblemon Dialogue GUI textures and animates the gibber typewriter at whatever speed you've set
Clicking buttons in the preview navigates the dialogue so you can walk through the whole flow without loading the game
Warnings for broken page references, unreachable pages and loops before you export

**MoLang support** — initializationAction, q.player.data flags, all input types (options, auto-continue, text input, none)
Rename a page ID and all set_page() references update automatically

Import existing dialogue JSONs, export clean ones

Some things worth knowing:

Auto-continue pages show a live countdown in the preview
q.player.data keys get tracked in a sidebar bank as you build — click any key to copy it
Right-click any node to duplicate or delete it
**This entire tool was generated with Claude. I am repeating this so it is clear. Use at your own risk. You can submit issues here and I will attempt to fix them but this will not be guaranteed. 
**
