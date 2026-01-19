Import('RTT_ROOT')
Import('rtconfig')
from building import *
import os

cwd = GetCurrentDir()

path = []

src = Split("""
""")

# add pin drivers.
if GetDepend('USING_CJSON'):
    src += ['cJSON/cJSON.c', 'cJSON/cJSON_Utils.c']
    path += ['cJSON/cJSON.h', 'cJSON/cJSON_Utils.h']

if GetDepend('USING_PROTOBUF'):
    src += ['nanopd/pb_encode.c', 'nanopd/pb_decode.c', 'nanopd/pb_common.c']
    path += ['nanopd']
    proto_generated_path = os.path.join('../protoc_generated')
    if not os.path.exists(proto_generated_path):
        os.makedirs(proto_generated_path)
    proto_dir = os.path.join(cwd, '../proto')
    if not os.path.exists(proto_dir):
        print("proto dir not exist!")
        exit(1)
    generator_exec_path = os.path.join(cwd, 'nanopd/generator/nanopb_generator.py')
    cmd_str = 'cd {} && python {} *.proto -D {}'.format(proto_dir, generator_exec_path, proto_generated_path)

    os.system(cmd_str)

    src += Glob(proto_generated_path + '/*.c')
    path += [proto_generated_path]

if GetDepend('USING_UTHASH'):
    path += ['uthash/src/']

if GetDepend('USING_XLINK'):
    path += ['xlink/','../xlink_generator/']
    generator_exec_path = os.path.join(cwd, 'xlink/tools/xlink_generator.py')
    cmd_str = 'python {} -i ../xlink_messagedef/project.json -o ../xlink_generator'.format(generator_exec_path)
    os.system(cmd_str)

group = DefineGroup('mcu_components', src, depend = [''], CPPPATH = path)

Return('group')
