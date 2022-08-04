# whatnpm
是什么 node 包管理器? 

-- 此项目用于猜测你的项目之前使用了什么包管理器.

## 为什么开发此项目
众所周知道 node 包管理器有很多, 例如: npm cnpm pnpm yarn yarn2, tyarn...

大部分的情况下, 他们都可以混合使用. 这是由于 nodejs 的 require 有很强的兼容性.

但是后来各个包管理器为了追求极致的安装速度, 会导致兼容性出现问题, 例如幽灵依赖, 虚拟文件...

所以这时候混合使用就可能出现问题.


## 如何锁定包管理器
- package.packageManager

### 相似项目
- [ni](https://www.npmjs.com/package/@antfu/ni) 期望统一包管理器的命令行参数, 通过 `*.lock` 文件或者 package.packageManager 来猜测应该调用什么包管理器.
- [only-allow](https://github.com/pnpm/only-allow) 强制在项目中使用特定的包管理器.
- https://www.npmjs.com/package/which-pm-runs
- https://github.com/zkochan/packages/tree/main/preferred-pm


## 如何实现
检测每个包管理器安装后的一些特征, 例如:
- lockfile
- package.packageManager
- node_modules 


- package.json
  ``` json
  {
    "dependencies": {
      "which-pm-runs": "^1.1.0"
    }
  }
  ```
- `yarn` v1.22.19
  - lockfile
    - yarn.lock
      - `yarn lockfile v1`
  - node_modules
    - .yarn-integrity
- `npm i` v8.15.1
  - lockfile
    - package-lock.json
      - `"lockfileVersion": 2`
  - node_modules
    - .package-lock.json
- `cnpm i` v7.1.0
  - lockfile
    - .package_versions.json
  - node_modules
    - .package-lock.json