### Vue.js的template编译的理解

简而言之，就是先转化成AST树，再得到的render函数返回VNode（Vue的虚拟DOM节点）

详情步骤：

    首先，通过compile编译器把template编译成AST语法树（abstract syntax tree 
    即源代码的抽象语法结构的树状表现形式），compile是createCompiler的返回值，
    createCompiler是用以创建编译器的。另外compile还负责合并option。
    
    然后，AST会经过generate（将AST语法树转化成render funtion字符串的过程）得到render函数，
    render的返回值是VNode，VNode是Vue的虚拟DOM节点，里面有（标签名、子节点、文本等等）