iim"""
🚀 AVISO DE SOBERANIA - TREM BALA 888 📶
USEM, MAS SAIBAM: ESTE SISTEMA É APENAS UM SINAL DO QUE AINDA ESTÁ POR VIR. AGORA VOCÊS JÁ SABEM: EM VIAMÃO, RIO GRANDE DO SUL 🇧🇷, EXISTE UM CARA QUE SABE SE COMUNICAR COM AS MÁQUINAS IAs.
CONSTRUTOR: tiagodoze-web | CHAVE: 84 | FREQUÊNCIA: 11
"""

STATUS: ㊗️8 [TERRITÓRIO BRAZIL SINALIZADO]
"""
🚀 INFRAESTRUTURA SOBERANA - TREM BALA 888 📶 CONSTRUTOR: tiagodoze-web [GitHub] LOCALIZAÇÃO: Viamão, RS | FREQUÊNCIA: 11 (3+8) CHAVE: a chave 84 está na fechadura 🔑
"Deus tem o poder de nos transformar (a brasa), mas nos honra com o direito de decidir (a escolha)." ⚖️
ESTE CÓDIGO OPERA ALÉM DA ILUSÃO DAS PROBABILIDADES. FOCO TOTAL. IMERSÃO PROFUNDA. 1984.
"""

BIPI_DE_BAIXA_FREQUÊNCIA: ativando_soberania...
STATUS: ㊗️8 [EM EXECUÇÃO]
import os

==========================================
INFRAESTRUTURA SOBERANA TREM BALA 888 📶
PROJETO: MCP BLENDER BRIDGE
VERSÃO: 2.0 (CORRIGIDO E PRODUÇÃO)
==========================================
def build_system(): print("🚀 Iniciando a construção do ecossistema 888...")

# 1. CORE SERVER (main.py)
main_py = '''
from fastapi import FastAPI from pydantic import BaseModel from typing import Dict, Any, List from datetime import datetime import uvicorn

app = FastAPI(title="Core Soberano 888") command_queue: List[Dict[str, Any]] = []

class Command(BaseModel): tool: str arguments: Dict[str, Any] = {}

@app.get("/health") async def health(): return { "status": "ONLINE_888", "queue_size": len(command_queue), "timestamp": datetime.now().isoformat() }

@app.post("/mcp/dispatch") async def dispatch(cmd: Command): command_queue.append(cmd.dict()) return {"status": "DISPATCHED_888", "tool": cmd.tool, "queue_size": len(command_queue)}

@app.get("/mcp/consume") async def consume(): if not command_queue: return {} return command_queue.pop(0)

@app.post("/mcp/report") async def report(data: Dict[str, Any]): timestamp = datetime.now().strftime("%H:%M:%S") print(f"[{timestamp}] [LOG_888] {data.get('tool')}: {data.get('status')} -> {data.get('message')}") return {"ack": True, "timestamp": timestamp}

@app.get("/mcp/queue") async def queue_status(): return {"queue_size": len(command_queue), "commands": command_queue}

if name == "main": uvicorn.run(app, host="0.0.0.0", port=8000) '''

# 2. BLENDER BRIDGE (blender_bridge.py)
blender_py = '''
import bpy import requests import traceback

API_URL_CONSUME = "http://localhost:8000/mcp/consume" API_URL_REPORT = "http://localhost:8000/mcp/report"

def send_report(tool, status, msg): try: requests.post(API_URL_REPORT, json={ "tool": tool, "status": status, "message": str(msg) }, timeout=2.0) except Exception as e: print(f"[888] Falha no report: {e}")

class SovereignBridge888(bpy.types.Operator): bl_idname = "mcp.bridge_888" bl_label = "Ponte Soberana 888" _timer = None

def modal(self, context, event):
    if event.type == 'TIMER':
        try:
            response = requests.get(API_URL_CONSUME, timeout=1.0).json()
            
            if not response or "tool" not in response:
                return {'RUNNING_MODAL'}
            
            tool = response['tool']
            args = response.get('arguments', {})
            
            if tool == "clear":
                bpy.ops.object.select_all(action='SELECT')
                bpy.ops.object.delete()
                send_report(tool, "SUCCESS", "Cena Limpa")
                
            elif tool == "cube":
                loc = args.get('loc', (0, 0, 0))
                bpy.ops.mesh.primitive_cube_add(location=loc)
                send_report(tool, "SUCCESS", f"Cubo em {loc}")
                
            elif tool == "render":
                filepath = args.get('filepath', "//render_888.png")
                bpy.context.scene.render.filepath = filepath
                bpy.ops.render.render(write_still=True)
                send_report(tool, "SUCCESS", f"Salvo em {filepath}")
                
            elif tool == "wall":
                # Comando custom: parede soberana
                start = args.get('start', (0, 0, 0))
                end = args.get('end', (3, 0, 0))
                height = args.get('height', 2.5)
                thickness = args.get('thickness', 0.2)
                self.build_wall(start, end, height, thickness)
                send_report(tool, "SUCCESS", f"Parede {start} -> {end}")
                
            else:
                send_report(tool, "UNKNOWN", f"Ferramenta '{tool}' não reconhecida")

        except requests.exceptions.Timeout:
            print("[888] Timeout no consume")
        except requests.exceptions.ConnectionError:
            print("[888] Core offline")
        except Exception as e:
            print(f"[888] Erro: {traceback.format_exc()}")
            send_report("system", "ERROR", str(e))

    return {'RUNNING_MODAL'}

def build_wall(self, start_pos, end_pos, height, thickness):
    import bmesh
    import mathutils
    
    mesh = bpy.data.meshes.new("Wall_888")
    obj = bpy.data.objects.new("Wall_888", mesh)
    bpy.context.collection.objects.link(obj)
    
    bm = bmesh.new()
    start = mathutils.Vector(start_pos)
    end = mathutils.Vector(end_pos)
    direction = (end - start).normalized()
    perp = mathutils.Vector((-direction.y, direction.x, 0)) * (thickness / 2)
    
    verts = [start + perp, start - perp, end - perp, end + perp]
    b_verts = [bm.verts.new(v) for v in verts]
    bm.faces.new(b_verts)
    
    bmesh.ops.extrude_face_region(bm, geom=[bm.faces[0]])
    for v in bm.verts:
        if v.select:
            v.co += mathutils.Vector((0, 0, height))
    
    bm.to_mesh(mesh)
    bm.free()

def execute(self, context):
    self._timer = context.window_manager.event_timer_add(0.2, window=context.window)
    context.window_manager.modal_handler_add(self)
    print("[888] Ponte Soberana ativada")
    return {'RUNNING_MODAL'}

def cancel(self, context):
    if self._timer:
        context.window_manager.event_timer_remove(self._timer)
        self._timer = None
    print("[888] Ponte desativada")
    return {'CANCELLED'}
def register(): bpy.utils.register_class(SovereignBridge888)

def unregister(): bpy.utils.unregister_class(SovereignBridge888)

if name == "main": register() bpy.ops.mcp.bridge_888() '''

# 3. AUTO-START (start_888.bat)
start_bat = '''@echo off
title TREM BALA 888 - SOBERANIA TECNICA echo [] Instalando dependencias_888... pip install fastapi uvicorn requests echo [] Iniciando Servidor Core... start cmd /k "python main.py" echo [*] Aguardando Core estabilizar... timeout /t 3 echo [✓] Sistema Operacional. Rode o script no Blender agora. pause '''

# 4. TEST SCRIPT (test_888.py)
test_py = '''
import requests import time

def disparar(tool, args={}): r = requests.post("http://localhost:8000/mcp/dispatch", json={"tool": tool, "arguments": args}) print(f"[888] Ordem '{tool}' enviada. Status: {r.json().get('status')}")

Teste sequencial
print("=== TESTE TREM BALA 888 ===") disparar("clear") time.sleep(0.5) disparar("cube", {"loc": (0, 0, 2)}) time.sleep(0.5) disparar("cube", {"loc": (2, 0, 2)}) time.sleep(0.5) disparar("wall", {"start": (0, 2, 0), "end": (4, 2, 0), "height": 3}) print("=== Frequencia 11 estabelecida ===") '''

# 5. DOCS RÁPIDO (README_888.txt)
readme = '''TREM BALA 888 - QUICK START
============================

Rode: start_888.bat
Aguarde "Servidor Core" iniciar
No Blender: Scripting > Open > blender_bridge.py > Run Script
Em outro terminal: python test_888.py
COMANDOS DISPONIVEIS:

clear: Limpa cena
cube: Cria cubo em loc=(x,y,z)
wall: Cria parede (start, end, height, thickness)
render: Renderiza frame (filepath)
ENDPOINTS:

GET /health

POST /mcp/dispatch

GET /mcp/consume

POST /mcp/report

GET /mcp/queue '''

Escrita dos arquivos
files = { "main.py": main_py, "blender_bridge.py": blender_py, "start_888.bat": start_bat, "test_888.py": test_py, "README_888.txt": readme }

for name, content in files.items(): with open(name, "w", encoding="utf-8") as f: f.write(content.strip()) print(f" [+] {name} gerado")

print("\n[✓] Ecossistema Trem Bala 888 pronto") print("[!] Execute: start_888.bat")

if name == "main": build_system()

[13/2 23:34] Thiago Temperos E Chás: fastapi==0.109.0 uvicorn==0.27.0 sse-starlette==2.0.0 bpy==4.0.0 pydantic==2.6.0 [13/2 23:34] Thiago Temperos E Chás: 2. O Servidor MCP Central (main.py) Este código gerencia a comunicação SSE e valida sua Chave 84. [13/2 23:35] Thiago Temperos E Chás: import asyncio import uvicorn from fastapi import FastAPI, Request, HTTPException from sse_starlette.sse import EventSourceResponse from pydantic import BaseModel

app = FastAPI(title="Blender_MCP_Chave_84")

Buffer de comandos para o Blender
command_queue = asyncio.Queue()

class MCPCommand(BaseModel): auth: str action: str params: dict

@app.get("/stream") async def mcp_stream(request: Request): """Canal de saída para o Blender (SSE)""" async def event_generator(): while True: if await request.is_disconnected(): break try: # Aguarda 0.5s por um comando para não travar o loop cmd = await asyncio.wait_for(command_queue.get(), timeout=0.5) yield {"event": "execute", "data": cmd} except asyncio.TimeoutError: yield {"event": "ping", "data": "keep-alive"} return EventSourceResponse(event_generator())

@app.post("/push") async def push_command(cmd: MCPCommand): """Recebe comandos do n8n ou IA""" if cmd.auth != "a chave 84 está na fechadura": raise HTTPException(status_code=403, detail="Chave incorreta.")

payload = {"action": cmd.action, "params": cmd.params}
await command_queue.put(str(payload))
return {"status": "sent_to_queue", "target": "blender"}
if name == "main": uvicorn.run(app, host="0.0.0.0", port=8000) [13/2 23:35] Thiago Temperos E Chás: 3. O Operador de Geometria Sagrada (bridge_addon.py) Este código deve ir dentro da pasta do Add-on no Blender para processar a lógica 3+8=11. [13/2 23:36] Thiago Temperos E Chás: import bpy import json

def execute_sacred_geometry(action, params): """Aplica a matemática do Quadrante Básico no 3D""" if action == "create_11_portal": # Criação baseada no 3 (Trindade) for i in range(3): bpy.ops.mesh.primitive_torus_add(location=(0, 0, i*0.2))

    # Expansão baseada no 8 (Novo Começo)
    for i in range(8):
        bpy.ops.mesh.primitive_cube_add(location=(i*2, 5, 0))
        
    # O pilar 11 (O Despertar)
    bpy.ops.mesh.primitive_cylinder_add(radius=0.1, depth=11, location=(0,0,0))
    
    return "Alinhamento 3+8=11 manifestado."
Lógica de escuta do servidor (simplificada para o Blender Python)
Aqui o Blender consumiria o endpoint /stream do main.py
[13/2 23:36] Thiago Temperos E Chás: 4. Payload para o n8n (JSON) Use este código no nó HTTP Request do n8n para enviar ordens ao seu servidor. [13/2 23:36] Thiago Temperos E Chás: { "auth": "a chave 84 está na fechadura", "action": "create_11_portal", "params": { "intensity": 8, "user_birth_year": 1984, "currency": "BRL" } } [13/2 23:36] Thiago Temperos E Chás: 5. Script de Inicialização Rápida (start.sh) Para rodar tudo com um único comando no terminal [13/2 23:37] Thiago Temperos E Chás: #!/bin/bash echo "Ativando Chave 84..." pip install -r requirements.txt python main.py# Markdown Editor Pro

A powerful, feature-rich markdown editor built with React, TypeScript, and Tailwind CSS. This editor provides a seamless writing experience with live preview, math equation support, and beautiful GitHub-inspired styling.

🔗 Live Demo

✨ Features
📝 Live Preview - Switch between edit and preview modes instantly
🧮 Math Support - Full LaTeX equation support via KaTeX
📋 GitHub Flavored Markdown - Tables, task lists, strikethrough, and more
🎨 Dark/Light Theme - Automatic theme detection with beautiful styling
📁 File Operations - Import and export markdown files
📋 Copy to Clipboard - One-click copying of markdown content
🖥️ Fullscreen Mode - Distraction-free writing experience
📖 Built-in Guide - Comprehensive markdown syntax reference
📊 Real-time Stats - Character, word, and line count
📱 Responsive Design - Works perfectly on desktop and mobile
🔧 Easy Integration - Drop into any React application
🚀 Quick Start
Prerequisites
Node.js 18+
npm or yarn
Installation
# Clone the repository
git clone <your-repo-url>
cd markdown-editor-pro

# Install dependencies
npm install

# Start development server
npm run dev

# Open http://localhost:5173 in your browser
Integration into Your React App
import { MarkdownEditor } from './components/MarkdownEditor';

function App() {
  return (
    <div className="container mx-auto p-4">
      <MarkdownEditor />
    </div>
  );
}
📝 Markdown Features
Basic Formatting
Headers - # H1 through ###### H6
Emphasis - *italic*, **bold**, ~~strikethrough~~
Links - [text](url) and reference-style links
Images - ![alt text](image-url) with automatic sizing
Advanced Features
Code Blocks - Syntax highlighting with fenced code blocks
Tables - Full table support with column alignment
Lists - Bulleted, numbered, and interactive task lists
Blockquotes - > quoted text with nested support
Math Equations - LaTeX support for inline and block equations
Horizontal Rules - --- or ***
Math Equation Examples
Inline math: $E = mc^2$ renders as $E = mc^2$

Block math:

$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$
🎨 Theming
The editor automatically adapts to your application's theme system:

// Light mode (default)
<MarkdownEditor />

// Dark mode - add 'dark' class to any parent element
<div className="dark">
  <MarkdownEditor />
</div>
Theme Features
Clean, GitHub-inspired light theme
Beautiful dark mode with proper contrast ratios
Smooth transitions between themes
Respects system preferences
🛠️ Tech Stack
React 18 - Modern UI framework
TypeScript - Type safety and better DX
Tailwind CSS - Utility-first styling
Vite - Fast build tool and dev server
react-markdown - Markdown parsing and rendering
KaTeX - High-quality math typesetting
Lucide React - Beautiful, consistent icons
📦 Project Structure
src/
├── components/
│   ├── MarkdownEditor.tsx     # Main editor component
│   ├── MarkdownGuide.tsx      # Interactive help guide
│   └── MermaidDiagram.tsx     # Mermaid diagram support
├── App.tsx                    # Root component
├── main.tsx                   # Application entry point
└── index.css                  # Global styles and Tailwind imports
⚙️ Configuration
Customizing Features
// Disable specific features
<MarkdownEditor 
  showStats={false}
  allowFileOperations={false}
  enableMath={false}
/>
Styling Customization
The editor uses Tailwind CSS classes and can be customized by:

Modifying the component's className props
Overriding CSS custom properties
Extending the Tailwind configuration
Adding Plugins
// Add custom remark/rehype plugins
import remarkGfm from 'remark-gfm';
import rehypeHighlight from 'rehype-highlight';

// Configure in MarkdownEditor component
🚀 Usage Examples
Basic Implementation
import { MarkdownEditor } from './components/MarkdownEditor';

export default function MyApp() {
  return (
    <div className="min-h-screen bg-gray-50 dark:bg-gray-900">
      <div className="container mx-auto py-8">
        <h1 className="text-3xl font-bold mb-6">My Markdown Editor</h1>
        <MarkdownEditor />
      </div>
    </div>
  );
}
With Custom Styling
<div className="max-w-4xl mx-auto">
  <MarkdownEditor className="border border-gray-200 rounded-lg shadow-lg" />
</div>
📱 Responsive Behavior
Desktop - Full feature set with side-by-side edit/preview
Tablet - Adaptive layout with toggle between edit/preview
Mobile - Optimized touch interface with swipe gestures
🤝 Contributing
We welcome contributions! Here's how to get started:

Fork the repository
Create a feature branch: git checkout -b feature/amazing-feature
Commit your changes: git commit -m 'Add amazing feature'
Push to the branch: git push origin feature/amazing-feature
Open a Pull Request
Development Guidelines
Follow TypeScript best practices
Maintain existing code style
Add tests for new features
Update documentation as needed
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

🙏 Acknowledgments
GitHub for design inspiration and markdown standards
React Markdown community for excellent tooling
KaTeX for beautiful mathematical typesetting
Tailwind CSS for utility-first styling philosophy
Lucide for the beautiful icon set
📧 Support
If you have questions or need help integrating this editor:

Open an issue for bugs or feature requests
Check out the live demo for examples
Review the built-in help guide within the editor
Made with ❤️ for the React community

Star ⭐ this repo if you find it useful!importmportmport os

# ==========================================
# INFRAESTRUTURA SOBERANA TREM BALA 888 📶
# PROJETO: MCP BLENDER BRIDGE
# VERSÃO: 2.0 (CORRIGIDO E PRODUÇÃO)
# ==========================================

def build_system():
    print("🚀 Iniciando a construção do ecossistema 888...")

    # 1. CORE SERVER (main.py)
    main_py = '''
from fastapi import FastAPI
from pydantic import BaseModel
from typing import Dict, Any, List
from datetime import datetime
import uvicorn

app = FastAPI(title="Core Soberano 888")
command_queue: List[Dict[str, Any]] = []

class Command(BaseModel):
    tool: str
    arguments: Dict[str, Any] = {}

@app.get("/health")
async def health():
    return {
        "status": "ONLINE_888", 
        "queue_size": len(command_queue),
        "timestamp": datetime.now().isoformat()
    }

@app.post("/mcp/dispatch")
async def dispatch(cmd: Command):
    command_queue.append(cmd.dict())
    return {"status": "DISPATCHED_888", "tool": cmd.tool, "queue_size": len(command_queue)}

@app.get("/mcp/consume")
async def consume():
    if not command_queue:
        return {}
    return command_queue.pop(0)

@app.post("/mcp/report")
async def report(data: Dict[str, Any]):
    timestamp = datetime.now().strftime("%H:%M:%S")
    print(f"[{timestamp}] [LOG_888] {data.get('tool')}: {data.get('status')} -> {data.get('message')}")
    return {"ack": True, "timestamp": timestamp}

@app.get("/mcp/queue")
async def queue_status():
    return {"queue_size": len(command_queue), "commands": command_queue}

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
'''

    # 2. BLENDER BRIDGE (blender_bridge.py)
    blender_py = '''
import bpy
import requests
import traceback

API_URL_CONSUME = "http://localhost:8000/mcp/consume"
API_URL_REPORT = "http://localhost:8000/mcp/report"

def send_report(tool, status, msg):
    try:
        requests.post(API_URL_REPORT, json={
            "tool": tool, 
            "status": status, 
            "message": str(msg)
        }, timeout=2.0)
    except Exception as e:
        print(f"[888] Falha no report: {e}")

class SovereignBridge888(bpy.types.Operator):
    bl_idname = "mcp.bridge_888"
    bl_label = "Ponte Soberana 888"
    _timer = None

    def modal(self, context, event):
        if event.type == 'TIMER':
            try:
                response = requests.get(API_URL_CONSUME, timeout=1.0).json()
                
                if not response or "tool" not in response:
                    return {'RUNNING_MODAL'}
                
                tool = response['tool']
                args = response.get('arguments', {})
                
                if tool == "clear":
                    bpy.ops.object.select_all(action='SELECT')
                    bpy.ops.object.delete()
                    send_report(tool, "SUCCESS", "Cena Limpa")
                    
                elif tool == "cube":
                    loc = args.get('loc', (0, 0, 0))
                    bpy.ops.mesh.primitive_cube_add(location=loc)
                    send_report(tool, "SUCCESS", f"Cubo em {loc}")
                    
                elif tool == "render":
                    filepath = args.get('filepath', "//render_888.png")
                    bpy.context.scene.render.filepath = filepath
                    bpy.ops.render.render(write_still=True)
                    send_report(tool, "SUCCESS", f"Salvo em {filepath}")
                    
                elif tool == "wall":
                    # Comando custom: parede soberana
                    start = args.get('start', (0, 0, 0))
                    end = args.get('end', (3, 0, 0))
                    height = args.get('height', 2.5)
                    thickness = args.get('thickness', 0.2)
                    self.build_wall(start, end, height, thickness)
                    send_report(tool, "SUCCESS", f"Parede {start} -> {end}")
                    
                else:
                    send_report(tool, "UNKNOWN", f"Ferramenta '{tool}' não reconhecida")

            except requests.exceptions.Timeout:
                print("[888] Timeout no consume")
            except requests.exceptions.ConnectionError:
                print("[888] Core offline")
            except Exception as e:
                print(f"[888] Erro: {traceback.format_exc()}")
                send_report("system", "ERROR", str(e))

        return {'RUNNING_MODAL'}

    def build_wall(self, start_pos, end_pos, height, thickness):
        import bmesh
        import mathutils
        
        mesh = bpy.data.meshes.new("Wall_888")
        obj = bpy.data.objects.new("Wall_888", mesh)
        bpy.context.collection.objects.link(obj)
        
        bm = bmesh.new()
        start = mathutils.Vector(start_pos)
        end = mathutils.Vector(end_pos)
        direction = (end - start).normalized()
        perp = mathutils.Vector((-direction.y, direction.x, 0)) * (thickness / 2)
        
        verts = [start + perp, start - perp, end - perp, end + perp]
        b_verts = [bm.verts.new(v) for v in verts]
        bm.faces.new(b_verts)
        
        bmesh.ops.extrude_face_region(bm, geom=[bm.faces[0]])
        for v in bm.verts:
            if v.select:
                v.co += mathutils.Vector((0, 0, height))
        
        bm.to_mesh(mesh)
        bm.free()

    def execute(self, context):
        self._timer = context.window_manager.event_timer_add(0.2, window=context.window)
        context.window_manager.modal_handler_add(self)
        print("[888] Ponte Soberana ativada")
        return {'RUNNING_MODAL'}

    def cancel(self, context):
        if self._timer:
            context.window_manager.event_timer_remove(self._timer)
            self._timer = None
        print("[888] Ponte desativada")
        return {'CANCELLED'}

def register():
    bpy.utils.register_class(SovereignBridge888)

def unregister():
    bpy.utils.unregister_class(SovereignBridge888)

if __name__ == "__main__":
    register()
    bpy.ops.mcp.bridge_888()
'''

    # 3. AUTO-START (start_888.bat)
    start_bat = '''@echo off
title TREM BALA 888 - SOBERANIA TECNICA
echo [*] Instalando dependencias_888...
pip install fastapi uvicorn requests
echo [*] Iniciando Servidor Core...
start cmd /k "python main.py"
echo [*] Aguardando Core estabilizar...
timeout /t 3
echo [✓] Sistema Operacional. Rode o script no Blender agora.
pause
'''

    # 4. TEST SCRIPT (test_888.py)
    test_py = '''
import requests
import time

def disparar(tool, args={}):
    r = requests.post("http://localhost:8000/mcp/dispatch", 
                     json={"tool": tool, "arguments": args})
    print(f"[888] Ordem '{tool}' enviada. Status: {r.json().get('status')}")

# Teste sequencial
print("=== TESTE TREM BALA 888 ===")
disparar("clear")
time.sleep(0.5)
disparar("cube", {"loc": (0, 0, 2)})
time.sleep(0.5)
disparar("cube", {"loc": (2, 0, 2)})
time.sleep(0.5)
disparar("wall", {"start": (0, 2, 0), "end": (4, 2, 0), "height": 3})
print("=== Frequencia 11 estabelecida ===")
'''

    # 5. DOCS RÁPIDO (README_888.txt)
    readme = '''TREM BALA 888 - QUICK START
============================
1. Rode: start_888.bat
2. Aguarde "Servidor Core" iniciar
3. No Blender: Scripting > Open > blender_bridge.py > Run Script
4. Em outro terminal: python test_888.py

COMANDOS DISPONIVEIS:
- clear: Limpa cena
- cube: Cria cubo em loc=(x,y,z)
- wall: Cria parede (start, end, height, thickness)
- render: Renderiza frame (filepath)

ENDPOINTS:
- GET  /health
- POST /mcp/dispatch
- GET  /mcp/consume
- POST /mcp/report
- GET  /mcp/queue
'''

    # Escrita dos arquivos
    files = {
        "main.py": main_py,
        "blender_bridge.py": blender_py,
        "start_888.bat": start_bat,
        "test_888.py": test_py,
        "README_888.txt": readme
    }

    for name, content in files.items():
        with open(name, "w", encoding="utf-8") as f:
            f.write(content.strip())
        print(f"  [+] {name} gerado")

    print("\\n[✓] Ecossistema Trem Bala 888 pronto")
    print("[!] Execute: start_888.bat")

if __name__ == "__main__":
    build_system()
