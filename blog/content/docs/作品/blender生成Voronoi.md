
```tpl
import bpy
import random

# 设置画布大小
bpy.context.scene.render.resolution_x = 2048
bpy.context.scene.render.resolution_y = 2048

# 创建材质
mat = bpy.data.materials.new(name="VoronoiMaterial")
mat.use_nodes = True

# 获取节点树
tree = mat.node_tree

# 删除所有节点
for node in tree.nodes:
    tree.nodes.remove(node)

# 创建输入节点
input_node = tree.nodes.new(type="ShaderNodeTexVoronoi")
input_node.inputs[1].default_value = 1.0

# 创建输出节点
output_node = tree.nodes.new(type="ShaderNodeOutputMaterial")

# 连接节点
tree.links.new(input_node.outputs[0], output_node.inputs[0])

# 创建平面
bpy.ops.mesh.primitive_plane_add(size=2, location=(0, 0, 0))

# 将材质应用到平面
plane = bpy.context.object
plane.active_material = mat

# 渲染图像
bpy.ops.render.render(write_still=True)
```