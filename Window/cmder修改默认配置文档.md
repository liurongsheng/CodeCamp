# cmder修改默认配置文档

## 问题：标签窗口没有保存

在配置中 `启动-启动选项` 中选择 `自动保存/恢复打开过的标签页`

## 问题：输入会残留字符

通过更改默认的命令提示符可以解决

修改配置 `config\cmder_prompt_config.lua`

```config
prompt_lambSymbol = "λ" // 221218[64] {Stable}版本是在 22 行
```

修改为 `#`、`$` 都行

## 问题：将路径信息和提示符并为一行显示

```config
prompt_singleLine = false // 221218[64] {Stable}版本是在 30 行
```

修改为 true 就行

要让默认宽度小一点，修改配置 `vendor\clink.lua`

```config
if prompt_singleLine then
        cr = ' '
    end
```

修改 `cr = ' '` 为 `cr = ''`

找到

```config
clink.prompt.value = string.gsub(clink.prompt.value, "{hg}", " "..verbatim(result))
```

修改 `"{hg}", " "..verbatim(result)` 为 `"{hg}", ..verbatim(result)`
