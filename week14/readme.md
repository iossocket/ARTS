### ARTS

#### Algorithm
##### Sort an Array (Selection Sort)
Given an array of integers nums, sort the array in ascending order.

Example 1:
```
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
```
Example 2:
```
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

```java
public class SortArray {
    public List<Integer> selectionSort(int[] nums) {
        if (nums.length <= 1) {
            return convertArrayToList(nums);
        }
        for (int i = 0; i < nums.length; i++) {
            int minValue = nums[i];
            int minIndex = i;
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] < minValue) {
                    minValue = nums[j];
                    minIndex = j;
                }
            }
            if (i == minIndex) {
                continue;
            }
            int temp = nums[i];
            nums[i] = nums[minIndex];
            nums[minIndex] = temp;
        }
        return convertArrayToList(nums);
    }

    private List<Integer> convertArrayToList(int[] nums) {
        List<Integer> list = new ArrayList<>();
        for (int item : nums) {
            list.add(item);
        }
        return list;
    }
}
```

#### Review

原文链接：[Getting Started with SwiftUI Animations](https://www.raywenderlich.com/5815412-getting-started-with-swiftui-animations)

[SwiftUI - 基础动画](https://www.jianshu.com/p/d200e7295cfc)

#### Tips

从这周开始，准备启动一个新的专题《React Native拆包实践》，目的是想完成jsbundle的拆分，分为基础包和业务包，从而实现js的按需加载，其一可以提高启动速度，其二可以变相实现一个App中同时容纳多个RN模块。

先来一个预热吧，当我们使用`react-native run-ios`或通过Xcode启动RN项目时，都会自动启动一个bundle server，用来在dev模式下加载js代码，那么这部分是如何实现的呢？使用Xcode开启RN项目，可以看到在`build phases`中有一步名为`Start Packager`的操作，其中有一段shell脚本，如下所示：

```shell
export RCT_METRO_PORT="${RCT_METRO_PORT:=8081}"
echo "export RCT_METRO_PORT=${RCT_METRO_PORT}" > "${SRCROOT}/../node_modules/react-native/scripts/.packager.env"
if [ -z "${RCT_NO_LAUNCH_PACKAGER+xxx}" ] ; then
  if nc -w 5 -z localhost ${RCT_METRO_PORT} ; then
    if ! curl -s "http://localhost:${RCT_METRO_PORT}/status" | grep -q "packager-status:running" ; then
      echo "Port ${RCT_METRO_PORT} already in use, packager is either not running or not running correctly"
      exit 2
    fi
  else
    open "$SRCROOT/../node_modules/react-native/scripts/launchPackager.command" || echo "Can't start packager automatically"
  fi
fi
```

我们来逐行解释一些：
1. `export RCT_METRO_PORT="${RCT_METRO_PORT:=8081}"` 在当前session中声明一个环境变量`RCT_METRO_PORT`，也就是这个bundle server的端口号，定义为8081
2. `echo...` 将这个端口号写入了`.packager.env`中，用于后面使用这个端口号
3. `if [ -z "${RCT_NO_LAUNCH_PACKAGER+xxx}" ]` 检查是否声明了`RCT_NO_LAUNCH_PACKAGER+xxx`这个环境变量，`-z`用于判断这个变量的长度是否为0，如果为0则执行then后的脚本，这个环境变量的声明用于调用方不想要启动这个server，比如在构建production包时
4. `if nc -w 5 -z localhost ${RCT_METRO_PORT}` 当步骤3中没有声明那个环境变量时，将做这个检测。`nc -w 5 -z localhost 8081`：使用Natcat工具，`-w 5`扫描5秒，`-z localhost 8081`扫描localhost的8081端口。当这个端口已经被占用时，执行第5步，当没有被占用时，执行第7步
5. `if ! curl -s "http://localhost:${RCT_METRO_PORT}/status" | grep -q "packager-status:running"`，当端口被占用时，需要检测一下这个端口是不是被之前启动好的bundle server在使用（比如在之前已经运行了`npm run start`）。检测的方式是向`http://localhost:${RCT_METRO_PORT}/status`发送一个get请求，再由`| grep -q "packager-status:running"`看看response中是否包含`packager-status:running`。当不包含时执行步骤6
6. `echo "Port ${RCT_METRO_PORT} ..."`，输出一个log，之后就`exit 2`，此时也将break当前Xcode的build
7. `open "$SRCROOT/../node_modules/react-native/scripts/launchPackager.command" || echo "Can't start packager automatically"` 运行`launchPackager.command`，如果失败则输出一个log。
8. `launchPackager.command`是什么呢？代码如下
```shell
#!/bin/bash
# Copyright (c) Facebook, Inc. and its affiliates.
#
# This source code is licensed under the MIT license found in the
# LICENSE file in the root directory of this source tree.

# Set terminal title
echo -en "\\033]0;Metro Bundler\\a"
clear

THIS_DIR=$(cd -P "$(dirname "$(readlink "${BASH_SOURCE[0]}" || echo "${BASH_SOURCE[0]}")")" && pwd)

# shellcheck source=/dev/null
. "$THIS_DIR/packager.sh"

if [[ -z "$CI" ]]; then
  echo "Process terminated. Press <enter> to close the window"
  read -r
fi
```
其实就执行了当前目录下的另一个shell脚本packager.sh：
```shell
#!/bin/bash
# Copyright (c) Facebook, Inc. and its affiliates.
#
# This source code is licensed under the MIT license found in the
# LICENSE file in the root directory of this source tree.

# scripts directory
THIS_DIR=$(cd -P "$(dirname "$(readlink "${BASH_SOURCE[0]}" || echo "${BASH_SOURCE[0]}")")" && pwd)
REACT_NATIVE_ROOT="$THIS_DIR/.."
# Application root directory - General use case: react-native is a dependency
PROJECT_ROOT="$THIS_DIR/../../.."

# check and assign NODE_BINARY env
# shellcheck disable=SC1090
source "${THIS_DIR}/node-binary.sh"

# When running react-native tests, react-native doesn't live in node_modules but in the PROJECT_ROOT
if [ ! -d "$PROJECT_ROOT/node_modules/react-native" ];
then
  PROJECT_ROOT="$THIS_DIR/.."
fi
# Start packager from PROJECT_ROOT
cd "$PROJECT_ROOT" || exit
"$NODE_BINARY" "$REACT_NATIVE_ROOT/cli.js" start "$@"

```
做了一些check后，最后执行：`"$NODE_BINARY" "$REACT_NATIVE_ROOT/cli.js" start "$@"`，替换掉环境变量之后为：`node ../cli.js start`，$@指定的是传入的所有参数，而在调用packager.sh时没有任何参数。cli.js代码如下，这个cli其实就是Metro的CLI工具了：
```shell
#!/usr/bin/env node
/**
 * Copyright (c) Facebook, Inc. and its affiliates.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 *
 * @format
 */

'use strict';

var cli = require('@react-native-community/cli');

if (require.main === module) {
  cli.run();
}

module.exports = cli;
```

在下一节中我们来揭开Metro的神秘面纱。

#### Sharing

开始重新学backend，开始写一个系列文章：

Keycloak的第七篇 [Identity Provider](https://www.jianshu.com/p/069ce3f1147f)