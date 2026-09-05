# 1.主要命令
| 场景                  | 命令                    | 作用                                                         | 例子                                   |
| ------------------- | --------------------- | ---------------------------------------------------------- | ------------------------------------ |
| 初始化一个新 Python 项目    | `uv init`             | 创建项目骨架，通常包括 `pyproject.toml`、`.python-version`、示例代码等       | `uv init my-project`                 |
| 给项目添加依赖             | `uv add`              | 把依赖加入 `pyproject.toml`，更新 `uv.lock`，并同步项目环境                | `uv add requests`                    |
| 添加开发依赖              | `uv add --dev`        | 添加只用于开发/测试的依赖，如 `pytest`、`ruff`                            | `uv add --dev pytest`                |
| 删除项目依赖              | `uv remove`           | 从项目依赖声明中移除包，同时更新 `uv.lock` 和环境                             | `uv remove requests`                 |
| 同步项目环境              | `uv sync`             | 根据 `pyproject.toml` / `uv.lock` 创建或更新 `.venv`，让实际环境与锁文件一致  | `uv sync`                            |
| 在项目环境中运行命令          | `uv run`              | 自动使用项目对应的 Python 和虚拟环境执行命令，通常无需手动激活 `.venv`                | `uv run python main.py`              |
| 在项目环境中运行测试/CLI      | `uv run`              | 运行安装在项目依赖中的 CLI 工具                                         | `uv run pytest`                      |
| 生成或更新锁文件            | `uv lock`             | 根据 `pyproject.toml` 做依赖解析，将确定的依赖版本写入 `uv.lock`             | `uv lock`                            |
| 安装指定 Python 版本      | `uv python install`   | 下载并管理 Python 解释器，可替代部分 `pyenv` 使用场景                        | `uv python install 3.12`             |
| 固定项目 Python 版本      | `uv python pin`       | 指定当前项目默认使用的 Python 版本，通常写入 `.python-version`               | `uv python pin 3.12`                 |
| 临时运行 Python CLI 工具  | `uv tool run` / `uvx` | 在隔离环境中临时安装并运行工具，不需要把工具加入当前项目依赖；`uvx` 是 `uv tool run` 的快捷写法 | `uvx ruff check .`                   |
| 全局安装 CLI 工具         | `uv tool install`     | 把 Python CLI 工具安装为长期可用的全局命令，类似 `pipx install`              | `uv tool install ruff`               |
| 创建虚拟环境              | `uv venv`             | 创建传统 Python 虚拟环境，默认目录通常为 `.venv`                           | `uv venv`                            |
| 用指定 Python 创建虚拟环境   | `uv venv --python`    | 使用指定 Python 版本创建虚拟环境                                       | `uv venv --python 3.12`              |
| 以 pip 风格安装包         | `uv pip install`      | ==直接向当前虚拟环境安装包==，类似 `pip install`；主要管理“环境”，而不是项目依赖声明       | `uv pip install requests`            |
| 从 requirements 文件安装 | `uv pip install -r`   | 兼容传统 `requirements.txt` 工作流                                | `uv pip install -r requirements.txt` |

# 2.开发常用命令
`uv init`
`uv add`
`uv remove`
`uv run`
`uv sync`
`uv lock`
## 2.1. `uv init`
`uv init my-project`
创建一个 Python 项目骨架，一般会得到：
my-project/
├── .python-version
├── pyproject.toml
├── README.md
└── main.py

## 2.2. `uv add`
`uv add requests`
不只是 `pip install`
而是：
	修改 pyproject.toml
	       ↓
	重新解析依赖
	       ↓
	修改 uv.lock
	       ↓
	更新 .venv

## 2.3. `uv sync`
`uv sync`
把当前 `.venv` 同步成 `uv.lock` 所描述的状态，类似于 `pip install -r requirements.txt`

## 2.4. `uv lock`
`uv lock`
根据 `pyproject.toml`，重新做依赖解析，更新 uv.lock

例如：
```
pyproject.toml

requests>=2
fastapi>=0.110
```
uv 会递归处理：
```
requests
├── certifi
├── urllib3
├── idna
└── charset-normalizer

fastapi
├── starlette
├── pydantic
└── typing-extensions
```
然后挑出一套互相兼容的版本。

### 2.4.1. 为啥要有uv.lock?
`pyproject.toml`里面存：
```
dependencies = [
    "requests>=2",
]
```
但是满足条件的request可能会变，导致不同终端安装的request最终版本不同
lockfile解决：
声明：
requests >= 2
    ↓ resolver
锁定：
requests = X
urllib3 = Y
certifi = Z
...
因此项目要提交：
`pyproject.toml`
`uv.lock`

## 2.5. `uv venv`
替代 `python -m venv .venv`

