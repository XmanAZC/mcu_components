Import('RTT_ROOT')
Import('rtconfig')
from building import *

cwd = GetCurrentDir()

path = []

src = Split("""
""")

# add pin drivers.
if GetDepend('USING_CJSON'):
    src += ['cJSON/cJSON.c', 'cJSON/cJSON_Utils.c']
    path += ['cJSON/cJSON.h', 'cJSON/cJSON_Utils.h']

group = DefineGroup('mcu_components', src, depend = [''], CPPPATH = path)

Return('group')
