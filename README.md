routes指路由栈。

#### 支持缓存上一界面

1. A跳转至B，然后跳转至C， routes = [A, B, C]
2. C返回至B，C从栈中移除，B从缓存中恢复，routes = [A, B]
3. B返回至A，B从栈中移除，A从缓存中恢复，routes = [A]
4. A跳转至B，B重新创建，不从缓存中恢复，routes = [A, B];

#### 支持同一界面有多个实例

1. A跳转至B，然后又跳转至 A，routes = [A, B, A]。两个A是不同的实例，可以拥有不同的状态;
2. A返回至B，B从缓存中恢复，routes = [A, B, A];
3. B返回至A，routes = [A]

#### 支持缓存tab下的各个界面(假设tab下有A，B，C三个界面)

1. 当前是D界面，D进入A，routes = [D, A]
2. A激活B，B激活C，routes = [D, [A, B, C]], 被激活的界面如果在当前激活栈(当前是[A, B, C])中存在那就直接从栈中恢复，不存在就创建
3. C激活B， routes = [D, [A, C, B]],  栈顶是当前被激活的界面。
4. B进入E，routes = [D, [A, C, B], E]
5. E返回, routes =  [D, [A, C, B]]
6. 再返回 [D]

