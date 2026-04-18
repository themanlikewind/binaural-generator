# 双耳节拍生成器

双耳节拍生成器是一个Python工具，用于创建双耳节拍音频（WAV或FLAC格式），旨在
影响不同的脑波状态。通过YAML脚本配置精确的频率模式来针对特定的心理状态，
如专注、放松、冥想或睡眠。功能包括平滑的频率过渡、音量淡入淡出以及可选的背景
噪声混合（标准类型如白/粉红/棕色、高级类型如蓝/紫罗兰/灰色、以及自然声音如雨声/海浪声）。
可通过命令行或交互式网页界面访问，包含一个预配置脚本库用于常见用例。

## 目录

- [双耳节拍生成器](#双耳节拍生成器)
  - [目录](#目录)
  - [描述](#描述)
  - [背景](#背景)
    - [什么是双耳节拍？](#什么是双耳节拍)
    - [背景噪声类型](#背景噪声类型)
      - [标准噪声类型](#标准噪声类型)
      - [高级噪声类型](#高级噪声类型)
      - [自然声音](#自然声音)
    - [脑波开导](#脑波开导)
    - [脑波状态](#脑波状态)
  - [科学研究](#科学研究)
  - [安装](#安装)
    - [需求](#需求)
    - [从PyPi安装](#从pypi安装)
    - [从源代码安装](#从源代码安装)
  - [贡献](#贡献)
  - [使用方法](#使用方法)
    - [网页界面](#网页界面)
    - [命令行界面](#命令行界面)
  - [YAML脚本格式](#yaml脚本格式)
  - [脚本库](#脚本库)
    - [标准脚本](#标准脚本)
    - [带专门噪声的高级脚本](#带专门噪声的高级脚本)
  - [文件结构](#文件结构)
  - [资源](#资源)
    - [进阅读](#进一步阅读)
    - [参考文献](#参考文献)
  - [许可证](#许可证)

## 描述

此工具读取定义双耳节拍频率序列的YAML脚本，包含时长、可选的音量淡入淡出和可选的背景噪声设置。
然后根据该序列创建音频文件。支持WAV和FLAC两种输出格式。允许稳定的频率段、频率之间的平滑过渡以及
每个段的逐渐淡入/淡出。

该程序使用可配置的基础载波频率（默认为100 Hz）并创建立体声音频。
左右声道之间的频率差异产生双耳节拍效果，旨在影响脑波活动。背景噪声（如果配置）
将相等地添加到两个声道。

**注意：** YAML配置中的所有时长值（即duration、fade_in_duration和fade_out_duration）
均以秒为单位指定。

## 背景

### 什么是双耳节拍？

双耳节拍是指当两个略有不同的频率分别呈现给每只耳朵时所感知的听觉幻觉。
大脑检测这两个频率之间的相位差异并试图调和这种差异，从而产生一种第三个"节拍"频率的感觉，
其值等于两个音调之间的差异。

例如，如果向左耳呈现100 Hz的音调，向右耳呈现110 Hz的音调，
大脑就会感知到10 Hz的双耳节拍。这个感知频率对应于特定的脑波模式。

### 背景噪声类型

#### 标准噪声类型

- **白噪声**：在所有可听频率上包含相等的能量。听起来像嘶嘶声（例如，静电、风扇）。
- **粉红噪声**：能量随频率增加而减少（具体为每八度3dB）。听起来比白噪声更深沉（例如，稳定的降雨、风吹）。
- **棕色噪声（布朗/红噪声）**：能量比粉红噪声下降更陡峭（每八度6dB）。听起来更深沉（例如，强大的瀑布、雷声隆隆）。

#### 高级噪声类型

- **蓝噪声（天蓝色噪声）**：能量随频率增加而增加（具体为每八度3dB）。
  比白噪声具有更多的高频内容，创建更"明亮"的声音。
- **紫罗兰噪声（紫色噪声）**：能量随频率急剧增加（每八度6dB）。强调高频，
  创建"尖锐"或"嘶嘶"的声音。
- **灰噪声**：经过滤波以匹配人耳频率响应的白噪声。强调人类听觉最敏感的频率（2-5 kHz），
  创建感知上平衡的声音。

#### 自然声音

- **雨声**：自然降雨声模拟，提供平静而一致的音频背景。帮助掩盖外部干扰，同时创建舒缓的环境。
- **海浪**：模拟海浪有节奏的声音，结合低频隆隆声和定期的浪峰。创建动态而平静的自然声景。

添加背景噪声可以帮助掩盖令人分心的环保噪声或提供持续的听觉背景。
不同的噪声类型可能基于其频率特性对不同用例有益。

### 脑波开导

脑波开导是指大脑对有节奏的感官刺激（如声音或光脉冲）的电反应。
当大脑受到与特定脑波状态对应的频率的刺激时，倾向于使其电活动与该频率同步——
一个称为"频率跟随反应"的过程。

双耳节拍是实现脑波开导的一种方法，可能有助于诱导与不同脑波频率相关联的特定精神状态。

### 脑波状态

- **伽玛波（30-100 Hz）**：最快的脑波，与高级认知功能相关，如感官整合、
  集中注意力和高级心理处理。伽玛活动在将来自不同脑区的信息结合在一起方面起关键作用，
  通常在达到顶峰集中注意力和某些冥想状态期间增强。
- **贝塔波（13-30 Hz）**：警觉、专注、积极思考、问题解决。
  *注意*：较高的贝塔（例如18-30 Hz）可能与压力或焦虑相关，
  而较低的贝塔（12-15 Hz）与放松的专注相关。
- **阿尔法波（8-12 Hz）**：放松、冷静、轻度冥想、白日梦和被动注意力
  （例如闭眼或正念练习）。充当意识（贝塔）和潜意识（西塔）状态之间的桥梁。
- **西塔波（4-7 Hz）**：深度冥想、创意、直觉、嗜睡（第1阶段NREM睡眠）和浅睡眠（第2阶段NREM）。
- **德尔塔波（0.5-4 Hz）**：深度、无梦睡眠（NREM第3-4阶段，"慢波睡眠"）、
  身体愈合和再生。在恢复性睡眠中占主导，对免疫功能和记忆巩固至关重要。

*注意*：虽然西塔波在REM睡眠中出现，但它们不是主导模式。REM以混合频率活动
（包括类贝塔波）为特征，因为梦境期间脑活动增强。西塔在睡前放松和早期睡眠阶段更为突出。

## 科学研究

对双耳节拍的研究显示结果混合，但几项研究表明潜在的好处：

- **压力缓解**：一些研究表明，阿尔法频率范围内的双耳节拍可能有助于减少焦虑和压力
  ([Wahbeh et al., 2007](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5370608/))
- **认知增强**：研究表明注意力、工作记忆和其他认知功能可能改善
  ([Kraus & Porubanová, 2015](https://www.sciencedirect.com/science/article/abs/pii/S1053810015300593))
- **睡眠质量**：德尔塔频率双耳节拍可能改善某些个体的睡眠质量
  ([Jirakittayakorn & Wongsawat, 2018](https://www.frontiersin.org/articles/10.3389/fnhum.2018.00387/full))

## 安装

### 需求

- Python 3.10+
- `pyproject.toml`中列出的依赖项（numpy、PyYAML、soundfile、scipy）。

### 从PyPi安装

```bash
pip install binaural-generator
```

### 从源代码安装

1. 克隆存储库：

    ```bash
    git clone https://github.com/ksylvan/binaural-generator.git
    ```

2. **使用提供的脚本自动设置**：

    ```bash
    ./bin/setup.sh
    source .venv/bin/activate
    ```

    如果尚未安装，这会安装`uv`，并使用它创建`.venv/`虚拟环境并安装所需的包。

    > 注意：如果使用VS Code，工作区配置为在打开文件夹时自动运行设置脚本。

## 贡献

- Fork存储库。
- 创建功能分支（`git checkout -b feature/awesome-feature`）。
- 使用类型提示和文档字符串编写清晰、简明的代码。
- 确保新功能已测试并添加适当的单元测试。
- 运行测试：

  ```bash
  pytest
  ```

  您还可以使用`--run-performance`标志来运行通常被跳过的标记为`performance`的测试。
  这些通常是被跳过的。

- 运行linters：

  ```bash
  pylint .
  ```

- 提交拉取请求，并清楚地描述您的更改。

## 使用方法

### 网页界面

为了获得更多交互式体验，请运行基于网页的用户界面：

安装Python包后（通过`pip install`或从源代码），只需运行：

```bash
binaural-webapp
```

这启动了一个基于Streamlit的网页界面，允许您：

- 通过视觉界面创建和编辑音频序列
- 加载示例配置
- 在生成完整文件之前预览音频
- 自定义背景噪声设置
- 下载生成的音频和配置文件

启动后，打开网页浏览器并导航至`http://localhost:8501`来访问界面。

### 命令行界面

类似地，运行CLI脚本：

```bash
binaural-generate [options] <path_to_script.yaml>
```

**参数：**

- `<path_to_script.yaml>`：定义双耳节拍序列和设置的YAML文件。
- `-o <output_file>`，`--output <output_file>`（可选）：指定输出音频文件路径。
  文件扩展名确定格式（`.wav`或`.flac`）并覆盖YAML中的`output_filename`。
- `-v`或`--verbose`（可选）：启用详细日志输出。
- `-p`或`--parallel`（可选）：使用并行处理以加快音频生成。
- `--threads` NUMBER：用于并行处理的线程数（默认为CPU数）
- `--version`：打印版本并退出。
- `-l`或`--list`：列出可用的内置脚本。

**示例：**

要使用提供的示例脚本（默认为FLAC输出）：

```bash
binaural-generate example_script.yaml
```

这将在`audio/`目录中生成`audio/example_fade_noise.flac`
（或在`example_script.yaml`中指定的文件名）。

要使用库中的预定义脚本之一并输出为WAV：

```bash
binaural-generate scripts/relaxation_alpha.yaml -o audio/relaxation_alpha.wav
```

这将在`audio/`目录中生成`relaxation_alpha.wav`，覆盖脚本中的默认名称。

要生成具有自定义名称的FLAC文件：

```bash
binaural-generate scripts/focus_beta.yaml -o my_focus_session.flac
```

您也可以在不使用完整路径的情况下引用内置脚本。
只需列出可用的脚本：

```plaintext
$ binaural-generate -l
Available scripts: in /Users/kayvan/src/TMP/.venv/lib/python3.12/site-packages/binaural_generator/scripts

  Creativity (Blue Noise): creativity_blue.yaml
  Creativity (Theta): creativity_theta.yaml
  Focus (Beta): focus_beta.yaml
  Focus (Gamma): focus_gamma.yaml
  Focus (Violet Noise): focus_violet.yaml
  Lucid Dreaming (Pink Noise): lucid_dream_pink_noise.yaml
  Lucid Dreaming: lucid_dreaming.yaml
  Meditation (Theta): meditation_theta.yaml
  Migraine Relief (Alpha/Theta/Delta): migraine_relief.yaml
  Relaxation (Alpha): relaxation_alpha.yaml
  Relaxation (Grey Noise): relaxation_grey.yaml
  Relaxation (Ocean): relaxation_ocean.yaml
  Relaxation (Rain): relaxation_rain.yaml
  Sleep (Delta): sleep_delta.yaml

usage: generate [-h] [-o OUTPUT] [-v] [-p] [--threads THREADS] [--version | -l] [script]
```

然后：

```plaintext
$ binaural-generate -p meditation_theta.yaml
2025-04-12 07:39:40,375 - INFO - Using script from scripts directory: /Users/kayvan/src/TMP/.venv/lib/python3.12/site-packages/binaural_generator/scripts/meditation_theta.yaml
2025-04-12 07:39:40,376 - INFO - Processing Audio for: Meditation (Theta)
2025-04-12 07:39:40,376 - INFO - Sample Rate: 44100 Hz
2025-04-12 07:39:40,376 - INFO - Base Frequency: 100.00 Hz
2025-04-12 07:39:40,376 - INFO - Using parallel processing for audio generation...
2025-04-12 07:39:40,376 - INFO - Preparing audio steps for parallel generation...
2025-04-12 07:39:40,376 - INFO - Starting parallel generation of beats and noise...
2025-04-12 07:39:40,879 - INFO - Beat segments generated and collected.
2025-04-12 07:39:40,968 - INFO - Beat segments combined (Duration from segments: 1800.00 seconds).
2025-04-12 07:39:40,969 - INFO - Skipping noise mixing (not generated or zero amplitude).
2025-04-12 07:39:41,105 - INFO - Audio sequence generated successfully in 0.73 seconds.
2025-04-12 07:39:41,287 - INFO - Writing audio file to: audio/meditation_theta.flac
2025-04-12 07:39:42,884 - INFO - Audio file 'meditation_theta.flac' (.flac format, 44100 Hz) created. Duration: 30m 0.00s.
2025-04-12 07:39:42,907 - INFO - Audio file saved successfully to 'audio/meditation_theta.flac'.
```

## YAML脚本格式

YAML脚本定义了音频生成的参数和序列。

**全局设置（可选）：**

- `title`：短标题（也在网页UI中显示）
- `base_frequency`：载波频率，单位为Hz（例如100）。默认：`100`。
- `sample_rate`：音频采样率，单位为Hz（例如44100）。默认：`44100`。
- `output_filename`：输出音频文件的默认名称（例如`"audio/my_session.flac"`或`"audio/my_session.wav"`）。
  扩展名（`.wav`或`.flac`）确定输出格式。默认：`"output.flac"`。
- `background_noise`（可选）：添加背景噪声的设置。
  - `type`：噪声类型。选项：
    - 标准：`"white"`、`"pink"`、`"brown"`
    - 高级：`"blue"`、`"violet"`、`"grey"`
    - 自然：`"rain"`、`"ocean"`
    - 无噪声：`"none"`
    - 默认：`"none"`。
  - `amplitude`：噪声的相对振幅（音量），从`0.0`（无声）到`1.0`（最大相对水平）。
    默认：`0.0`。双耳节拍信号在混合前缩放`(1 - amplitude)`以防止失真。

**步骤（必需）：**

一个在`steps:`键下的列表，其中每个项目定义一个音频段。每个步骤可以是以下类型之一：

- **`type: stable`**：保持恒定的双耳节拍频率。
- `frequency`：双耳节拍频率，单位为Hz。
- `duration`：此段的时长，单位为秒。
- `fade_in_duration`（可选）：步骤开始处线性音量淡入的时长，单位为秒。默认：`0.0`。
- `fade_out_duration`（可选）：步骤末尾线性音量淡出的时长，单位为秒。默认：`0.0`。

对于`transition`步骤类型，我们有以下内容：

- **`type: transition`**：线性改变双耳节拍频率。
- `start_frequency`：起始双耳节拍频率，单位为Hz。如果省略，
  它使用前一步骤的结束频率以实现平滑过渡（对于第一步不能省略）。
- `end_frequency`：结束双耳节拍频率，单位为Hz。
- `duration`：此过渡的时长，单位为秒。
- `fade_in_duration`（可选）：步骤开始处线性音量淡入的时长，单位为秒。默认：`0.0`。
- `fade_out_duration`（可选）：步骤末尾线性音量淡出的时长，单位为秒。默认：`0.0`。

**关于淡入淡出的重要说明：**

- 淡入淡出应用于步骤指定的`duration`内。
- 单个步骤的`fade_in_duration`和`fade_out_duration`之和不能超过步骤的`duration`。

**示例YAML（`example_script.yaml`）：**

```yaml
# 示例双耳节拍生成脚本，包含淡入淡出和背景噪声

# 全局设置
title: Example Binaural Beat Script
base_frequency: 100 # Hz（载波频率）
sample_rate: 44100 # Hz（音频采样率）
output_filename: "audio/example_fade_noise.flac" # 默认输出文件名

# 背景噪声设置（可选）
background_noise:
  type: "pink" # 噪声类型："white"、"pink"、"brown"、"blue"、"violet"、"grey"、"rain"、"ocean"或"none"
  amplitude: 0.15 # 相对振幅（0.0至1.0）

# 音频生成步骤序列（总时长：1500秒 = 25分钟）
steps:
  # 1. 贝塔阶段（稳定18 Hz节拍），带淡入
  - type: stable
    frequency: 18 # Hz（双耳节拍频率）
    duration: 180 # 秒（3分钟）
    fade_in_duration: 6 # 秒

  # 2. 从贝塔（18 Hz）过渡到阿尔法（10 Hz）
  - type: transition
    start_frequency: 18 # Hz（显式，可以隐含）
    end_frequency: 10 # Hz
    duration: 300 # 秒（5分钟）

  # 3. 从阿尔法（10 Hz）过渡到西塔（6 Hz），带淡入淡出
  - type: transition
    # start_frequency: 10（从前一步骤隐含）
    end_frequency: 6 # Hz
    duration: 300 # 秒（5分钟）
    fade_in_duration: 3 # 秒
    fade_out_duration: 3 # 秒

  # 4. 从西塔（6 Hz）过渡到德尔塔（2 Hz），带淡出
  - type: transition
    # start_frequency: 6（隐含）
    end_frequency: 2 # Hz
    duration: 420 # 秒（7分钟）
    fade_out_duration: 12 # 秒

  # 5. 从德尔塔（2 Hz）过渡到伽玛（40 Hz），带淡入淡出
  - type: transition
    # start_frequency: 2（隐含）
    end_frequency: 40 # Hz
    duration: 300 # 秒（5分钟）
    fade_in_duration: 6 # 秒
    fade_out_duration: 15 # 秒
```

## 脚本库

`binaural_generator/scripts/`目录中提供了常见用例的预定义YAML脚本集合。
大多数脚本默认为`.flac`输出。某些包含背景噪声，如下所述。

### 标准脚本

- **`binaural_generator/scripts/focus_beta.yaml`**：设计用于使用贝塔波（14-18 Hz）增强专注力和警觉性。
- **`binaural_generator/scripts/focus_gamma.yaml`**：针对使用伽玛波（40 Hz）的峰值专注力和问题解决。
- **`binaural_generator/scripts/meditation_theta.yaml`**：使用西塔波（6 Hz）促进深度冥想和自我反思。
- **`binaural_generator/scripts/relaxation_alpha.yaml`**：旨在使用阿尔法波（8-10 Hz）减少压力和促进冷静。
- **`binaural_generator/scripts/sleep_delta.yaml`**：使用德尔塔波（2 Hz）引导大脑进入深度睡眠状态。

### 带专门噪声的高级脚本

- **`binaural_generator/scripts/creativity_blue.yaml`**：创意流增强，使用西塔波（6-7.83 Hz）和蓝噪声以获得清晰度。
- **`binaural_generator/scripts/creativity_theta.yaml`**：旨在培养使用西塔波（7 Hz）的直觉和创意心态。
- **`binaural_generator/scripts/focus_violet.yaml`**：使用伽玛波（40 Hz）和紫罗兰噪声增强专注力以提高警觉性。
- **`binaural_generator/scripts/lucid_dream_pink_noise.yaml`**：85分钟脚本，使用粉红噪声诱导REM睡眠并增强清醒梦潜力。
- **`binaural_generator/scripts/lucid_dreaming.yaml`**：60分钟脚本，从阿尔法过渡到西塔再到伽玛，促进清醒梦状态。
- **`binaural_generator/scripts/migraine_relief.yaml`**：从阿尔法到西塔到德尔塔的逐步放松，以减轻偏头痛疼痛。
- **`binaural_generator/scripts/relaxation_grey.yaml`**：使用灰噪声进行阿尔法波放松，实现自然环境音。
- **`binaural_generator/scripts/relaxation_ocean.yaml`**：25分钟深度放松，使用阿尔法波和模拟海浪声。
- **`binaural_generator/scripts/relaxation_rain.yaml`**：20分钟放松序列，使用阿尔法波和雨声环境音。

您可以直接使用这些脚本、修改它们（例如添加`background_noise`），或使用`-o`命令行选项更改输出格式/名称。

WAV输出并添加噪声的使用示例（假设您修改脚本）：

```bash
# （首先，编辑binaural_generator/scripts/sleep_delta.yaml以添加background_noise部分）
binaural-generate binaural_generator/scripts/sleep_delta.yaml -o audio/sleep_delta_with_noise.wav
```

## 文件结构

```markdown
.github
└── workflows
    └── pypi-publish.yml：用于在主分支推送时构建和发布包到PyPI的GitHub Actions工作流。

.vscode
└── tasks.json：VS Code任务定义，用于环境设置、运行测试和linting。

bin
└── setup.sh：使用`uv`和虚拟环境设置开发环境的shell脚本。

binaural_generator
├── cli.py：具有参数解析和生成器工具音频生成函数的命令行界面。
├── core
│   ├── __init__.py
│   ├── constants.py：定义整个包中使用的默认值和常量参数。
│   ├── data_types.py：定义配置对象的数据类（例如AudioStep、NoiseConfig）
|   |                  并验证其参数。
│   ├── exceptions.py：定义特定于双耳生成器包的自定义异常类。
│   ├── fade.py：实现音频段的线性音量淡入和淡出逻辑。
│   ├── noise.py：包含各种背景噪声生成策略（白、粉红、棕色、蓝、
|   |             紫罗兰、灰色、雨、海洋）。
│   ├── parallel.py：提供使用线程并行生成音频步骤的工具，加快处理速度。
│   ├── tone_generator.py：双耳节拍音调生成的核心逻辑，处理频率过渡、
|   |                      应用淡入淡出、混合噪声和保存音频文件。
│   └── utils.py：包含用于加载、验证和解析YAML配置文件的实用函数。
├── scripts
│   ├── creativity_blue.yaml：创意流增强，使用西塔波（6-7.83 Hz）和蓝噪声。
│   ├── creativity_theta.yaml：使用西塔波（7 Hz）培养直觉和创意心态。
│   ├── focus_beta.yaml：使用贝塔波（14-18 Hz）增强专注力和警觉性。
│   ├── focus_gamma.yaml：使用伽玛波（40 Hz）针对峰值专注力和问题解决。
│   ├── focus_violet.yaml：使用伽玛波（40 Hz）和紫罗兰噪声增强专注力。
│   ├── lucid_dream_pink_noise.yaml：85分钟脚本，使用粉红噪声诱导REM睡眠并增强清醒梦潜力。
│   ├── lucid_dreaming.yaml：60分钟脚本，从阿尔法过渡到西塔再到伽玛以促进清醒梦状态。
│   ├── meditation_theta.yaml：30分钟深度冥想序列，从阿尔法（10 Hz）过渡到西塔（6 Hz）。
│   ├── migraine_relief.yaml：从阿尔法到西塔到德尔塔的逐步放松，以减轻偏头痛疼痛。
│   ├── relaxation_alpha.yaml：20分钟压力缓解序列，使用阿尔法波（8-10 Hz）。
│   ├── relaxation_grey.yaml：使用灰噪声进行阿尔法波放松，实现自然环境音。
│   ├── relaxation_ocean.yaml：25分钟深度放松，使用阿尔法波和模拟海浪声。
│   ├── relaxation_rain.yaml：20分钟放松序列，使用阿尔法波和雨声环境音。
│   └── sleep_delta.yaml：45分钟睡眠诱导，从阿尔法通过西塔过渡到德尔塔（2 Hz）。
├── webapp.py：配置并运行基于Streamlit的界面的网页应用程序启动脚本。
└── webui
    ├── __init__.py
    ├── components
    │   ├── __init__.py
    │   ├── audio_handlers.py：网页界面的音频生成和播放实用程序，管理预览和完整音频生成。
    │   ├── config_utils.py：网页界面的YAML配置加载、验证和处理实用程序。
    │   ├── sidebar.py：网页界面设置控制的侧边栏组件呈现。
    │   ├── step_editor.py：用于编辑和可视化单个音频序列步骤的UI组件。
    │   └── ui_utils.py：会话状态管理和界面呈现的常规UI实用函数。
    ├── constants.py：UI特定常量，包括脑波预设和频率范围。
    └── main.py：网页应用程序的主入口点，编排组件和布局。

conftest.py：Pytest配置文件，包含自定义标记和命令行选项。
cspell.json：代码拼写检查配置，带有专用术语的自定义字典。
example_script.yaml：示例YAML配置，演示各种双耳节拍功能。
LICENSE：包含版权信息和使用条款的MIT许可证文件。
pyproject.toml：项目配置，包含依赖项、脚本和开发工具设置。
README.md：项目文档，包含详细的使用说明和背景信息。

tests
├── test_common.py：测试模块间共享的通用测试实用程序和帮助函数。
├── test_data_types.py：验证约束和行为的数据类型类的单元测试。
├── test_fade.py：音频音量淡入淡出实现和边界情况的测试。
├── test_new_noise_types.py：蓝色、紫罗兰和灰色噪声等高级噪声类型的测试。
├── test_noise.py：标准噪声生成算法的核心测试。
├── test_ocean_noise.py：海浪声模拟的测试。
├── test_parallel.py：并行处理实现和线程管理的测试。
├── test_property_based.py：使用hypothesis进行属性测试，实现强大的测试覆盖。
├── test_rain_noise.py：雨声模拟算法的测试。
├── test_tone_generator.py：双耳节拍生成和频率过渡的测试。
└── test_utils.py：配置加载和实用函数的测试。

uv.lock：uv包管理器的依赖项锁定文件，包含精确版本。

```

## 资源

### 进一步阅读

- [双耳节拍的发现][discovery-binaural-beats]
- [Healthline - 双耳节拍：它们真的影响你的大脑吗？][healthline] - 讨论双耳节拍的潜在认知和情绪益处
- [睡眠基金会 - 双耳节拍和睡眠][sleep-foundation] - 检查双耳节拍对睡眠质量的影响
- [双耳节拍开导大脑？双耳节拍刺激效果的系统综述][plos-one-ruth-research] - 发表于2023年。

### 参考文献

- Oster, G. (1973). Auditory beats in the brain. Scientific American, 229(4), 94-102.
- Huang, T. L., & Charyton, C. (2008). A comprehensive review of the psychological effects of brainwave entrainment. Alternative Therapies in Health and Medicine, 14(5), 38-50.
- Le Scouarnec, R. P., Poirier, R. M., Owens, J. E., Gauthier, J., Taylor, A. G., & Foresman, P. A. (2001). Use of binaural beat tapes for treatment of anxiety: A pilot study. Alternative Therapies in Health and Medicine, 7(1), 58-63.
- Chaieb, L., Wilpert, E. C., Reber, T. P., & Fell, J. (2015). Auditory beat stimulation and its effects on cognition and mood states. Frontiers in Psychiatry, 6, 70.
- Wahbeh, H., Calabrese, C., & Zwickey, H. (2007). Binaural beat technology in humans: a pilot study to assess psychologic and physiologic effects. Journal of Alternative and Complementary Medicine, 13(1), 25-32.
- Kraus, J., & Porubanová, M. (2015). The effect of binaural beats on working memory capacity. Studia Psychologica, 57(2), 135-145.
- Jirakittayakorn, N., & Wongsawat, Y. (2018). A novel insight of effects of a 3-Hz binaural beat on sleep stages during sleep. Frontiers in Human Neuroscience, 12, 387.
- Stumbrys, T., Erlacher, D., & Schredl, M. (2014). Testing the potential of binaural beats to induce lucid dreams. Dreaming, 24(3), 208–217.
- Prinsloo, S., Lyle, R., & Sewell, D. (2018). Alpha-Theta Neurofeedback for Chronic Pain: A Pilot Study. Journal of Neurotherapy, 22(3), 193-211.

## 许可证

该项目根据MIT许可证获得许可 - 有关详细信息，请参阅LICENSE文件。

版权所有（c）2025 Kayvan Sylvan

[discovery-binaural-beats]: https://www.binauralbeatsmeditation.com/dr-gerald-oster-auditory-beats-in-the-brain/
[healthline]: https://www.healthline.com/health/binaural-beats
[sleep-foundation]: https://www.sleepfoundation.org/bedroom-environment/binaural-beats
[plos-one-ruth-research]: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0286023

