import os

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
